# Offerly website

The pages behind the Offerly app: the marketing page, the privacy policy, a
support page and the subscription terms. Plain HTML and one stylesheet. No
build step, no npm, nothing to install.

```
index.html     the marketing page
privacy.html   the privacy policy, same text as the one inside the app
support.html   how to reach me, and answers to the usual problems
terms.html     Apple's licence plus the subscription terms
404.html       shown when a link is wrong
styles.css     all of the styling
assets/        the app icon and the screenshots
sitemap.xml    the page list for Google
```

The colours and shadows are copied from the app's `Theme.swift`, so the site
and the app look like the same thing.

## Changing something

Open the file, edit it, save it. To see it before publishing:

```
python3 -m http.server 4319
```

Then open http://localhost:4319 in a browser.

## Publishing

The site lives in its own public repository because GitHub Pages will not
serve a private one for free. Pushing to `main` publishes it:

```
git add -A
git commit -m "what changed"
git push
```

It takes about a minute. The live address is
https://kaisse99.github.io/offerly/ and GitHub Pages is set to build from the
`main` branch, root folder.

If a push does not appear, check whether the build ran at all:

```
gh api repos/Kaisse99/offerly/pages/builds/latest --jq .status
```

## Things worth remembering

- These files also live in the app repository under `Website/`. Editing one
  copy means committing in both, or they drift apart.
- `privacy.html` must match `PolicyView.swift` in the app. If one changes, the
  other has to, version line at the bottom included.
- The App Store links use the app's Apple ID, `6758880781`.
- `googlec07bbc77a1e7c3b5.html` is there so Google Search Console can confirm
  the site is mine. Do not delete it.
