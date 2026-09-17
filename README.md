# Offerly website

Four static pages for the App Store listing and for anyone who looks the app up:

| File | Purpose | Where it is used |
|---|---|---|
| `index.html` | Marketing page | Marketing URL in App Store Connect |
| `privacy.html` | The in-app privacy policy, version 3.1 | **Privacy Policy URL** in App Information — required |
| `support.html` | Support and troubleshooting | **Support URL** in the version page — required |
| `terms.html` | Apple's standard EULA plus the subscription terms | Linked from the description and the paywall |
| `404.html` | Not-found page GitHub Pages serves automatically | — |

No build step, no dependencies, no JavaScript. `styles.css` carries the app's own palette,
radii and shadow recipes, lifted from `Views/Shared/Theme.swift`, so the site and the app
stay the same object. It follows the visitor's light or dark setting the way the app follows
the system one.

These files are not part of any Xcode target. Nothing here ships inside the app.

## Before publishing

1. The download buttons point at Apple ID `6758880781`, set on 2026-09-17. If the app
   is ever re-created in App Store Connect, that number changes in every page.

2. Decide the support address. Everything currently points at `privacy.offerly@gmail.com`.
   If a separate support inbox is made later, swap it the same way.

## Publishing on GitHub Pages

The app repository is private, and GitHub Pages will not serve a private repository on a
free plan, so the site goes in its own public repository. Only these files become public.

1. Create a **public** repository named `offerly` on GitHub, with no README and no
   `.gitignore`.

2. Push this folder to it as its own repository:

   ```
   cd Website
   git init -b main
   git add .
   git commit -m "Add the Offerly site"
   git remote add origin https://github.com/Kaisse99/offerly.git
   git push -u origin main
   ```

   That leaves a nested `.git` directory inside `Website/`, which the app repository
   ignores through the entry added to `.git/info/exclude`.

3. In the new repository: **Settings → Pages → Build and deployment → Source:
   Deploy from a branch**, branch `main`, folder `/ (root)`, then Save.

4. A minute later the site is live at **https://kaisse99.github.io/offerly/**. The pages
   already declare that address as their canonical URL; changing the repository name means
   changing the `<link rel="canonical">` and the Open Graph URLs to match.

Publishing an update is the same three commands from inside `Website/`: `git add -A`,
`git commit -m "..."`, `git push`.

## A custom domain, if one is ever bought

Add a file named `CNAME` containing only the domain, point the domain's DNS at
`kaisse99.github.io` with a CNAME record, then set the domain under Settings → Pages and
tick Enforce HTTPS. Then update the canonical and Open Graph URLs in all four pages.

## Keeping the policy honest

`privacy.html` is a copy of what `PolicyView.swift` renders in the app. When one changes the
other has to change with it, including the version line at the bottom of both.

## Previewing locally

```
python3 -m http.server 4319 --directory Website
```

Then open http://localhost:4319. Opening the files directly with `file://` works too, but
a server is closer to how GitHub Pages will serve them.
