# text

A dead-simple text editor that runs entirely in your browser.

- **Autosave** to `localStorage` as you type.
- **Save .txt** downloads your text as a file.
- **Copy as link** puts the text into a shareable URL (content lives in the
  link's `#` fragment, nothing is uploaded to a server).
- **PWA / offline** install it and it keeps working with no network.

## Live site

https://genkio.github.io/text/

## How it works

A single static `index.html` plus a service worker (`sw.js`), a web app
manifest, and icons. No build step.

### Sharing

"Copy as link" encodes the current text into the URL hash, e.g.
`https://genkio.github.io/text/#<encoded>`. Opening that link loads the text.
Because the content sits in the `#` fragment it never reaches any server. Very
long documents produce very long links (normal browser URL limits apply).

### Offline

The service worker precaches the app shell, so once visited it loads and runs
offline. When online it fetches the latest version and falls back to the cache
when you're not.

## Deployment

GitHub Pages serves the `main` branch from the root. Every push to `main` is
published automatically by GitHub's built-in Pages build - no GitHub Actions
workflow is needed for a static site like this.

One-time setup: **Settings -> Pages -> Build and deployment -> Source: Deploy
from a branch -> `main` / `/ (root)`**.
