---
title: "Favicon updated but the browser still shows the old icon — 5 fixes that actually work"
tags: webdev, css, pwa, beginners
published: false
canonical_url: https://arnavjhajharia.github.io/favikit/favicon-sizes/
---

You deployed a new favicon. Hard refresh. Still the old one. This is normal — browsers cache favicons **aggressively**, sometimes for days, independent of your HTML cache headers.

## 1. Cache-bust the URL

```html
<link rel="icon" href="/favicon.ico?v=20261103" sizes="any">
```

Bump `v=` whenever the icon changes. Same for PNG favicons.

## 2. Ship every size, not just one PNG

Safari wants **apple-touch-icon** (180×180). Android/PWA wants **192** and **512** in the manifest. Windows still likes a real **multi-resolution `.ico`**. Missing sizes fall back to old cached files.

Full checklist (sizes + cache): [Favicon sizes in 2026](https://arnavjhajharia.github.io/favikit/favicon-sizes/#favicon-cache).

## 3. Clear site data (for your own QA)

Chrome → DevTools → Application → Clear storage → **including cached images**. Or test in a fresh profile / incognito without an old visit.

## 4. `favicon.ico` at the domain root

Some clients request `/favicon.ico` before parsing your HTML. If that file is stale on the CDN, you will not see updates until it expires.

## 5. Manifest `icons` must match deployed files

If `site.webmanifest` points at `/icon-192.png` but you only uploaded `android-chrome-192x192.png`, the PWA install path keeps an old icon.

---

## Generate the full set locally (no upload)

[Favikit](https://arnavjhajharia.github.io/favikit/) builds a proper `.ico`, all PNG sizes, manifest, and a paste-ready `<head>` block in the browser — nothing sent to a server. Handy when you are iterating and cache-busting every deploy.

_Disclosure: AI-assisted build; MIT [repo](https://github.com/arnavjhajharia/favikit)._
