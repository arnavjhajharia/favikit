# Favikit 🔒

**A private, in-browser favicon & app-icon generator. Nothing you drop ever leaves your device.**

👉 **Live: https://arnavjhajharia.github.io/favikit/**

Most favicon generators upload your image to a server. Favikit does everything client-side with
`<canvas>` — open your browser's network tab and watch: zero uploads.

## What you get from one image
- `favicon.ico` — a **real multi-resolution ICO** (16/32/48), not a renamed PNG
- `favicon-16/32/48.png`
- `apple-touch-icon.png` (180×180)
- `android-chrome-192x192.png` and `512x512.png`
- `site.webmanifest` (valid PWA manifest)
- A paste-ready `<head>` HTML snippet

Plus live controls for background, padding, and corner rounding, with an instant preview.

## Why it's different
- **Truly private** — no upload, no account, no tracking, no ads.
- **A correct `.ico`** — builds a proper ICO that embeds PNG frames, which Windows and older
  browsers accept. Many "generators" just rename a PNG.
- **Complete and current** — Apple, Android/PWA, manifest, and the exact markup. Nothing left to look up.

## Tech
Single static `index.html`. No build step. [JSZip](https://stuk.github.io/jszip/) (CDN) packs the
download. Hosted free on GitHub Pages.

MIT licensed. Contributions welcome.
