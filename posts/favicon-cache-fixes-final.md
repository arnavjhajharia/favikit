You deployed a new favicon, hard-refreshed, and the tab still shows the old one. That is normal: browsers keep favicons in their own cache (Chrome, for example, stores them in a separate favicon database), so a page reload often doesn't re-fetch the icon.

Here are the fixes, roughly in the order worth trying.

## 1. Cache-bust the icon URL

```html
<link rel="icon" href="/favicon.ico?v=2" sizes="any">
<link rel="icon" href="/icon.svg?v=2" type="image/svg+xml">
<link rel="apple-touch-icon" href="/apple-touch-icon.png?v=2">
```

Bump `v=` every time the icon changes. A new URL is a new cache entry, so the browser has to fetch it.

## 2. Open the icon file directly

Visit `https://yoursite.com/favicon.ico` in a tab and hard-reload that tab (Cmd/Ctrl+Shift+R). That often replaces the cached copy faster than reloading the page. A fresh browser profile or a private window is the quickest way to check what new visitors see.

## 3. Replace `/favicon.ico` at the domain root

Some browsers and tools request `/favicon.ico` at the root even when your HTML points somewhere else. If an old `favicon.ico` is still sitting at the root (or cached on your CDN), it keeps showing up. Replace it, or purge it from the CDN.

## 4. Ship the sizes each platform asks for

- `favicon.ico` (16 and 32 inside it) for classic browser tabs
- `apple-touch-icon.png` at 180x180 for iOS home screens
- 192x192 and 512x512 PNGs listed in `site.webmanifest` for Android / PWA installs

If one of these is missing, that platform falls back to whatever it had before, which looks like "the old icon won't go away".

## 5. Make the manifest point at files that exist

If `site.webmanifest` lists `/icon-192.png` but you deployed `android-chrome-192x192.png`, installed PWAs keep the old icon. Open the manifest URL in the browser and click each icon path to check.

## Reference

The full size table and a paste-ready `<head>` block are in this guide: [favicon sizes and cache fixes](https://arnavjhajharia.github.io/favikit/favicon-sizes/#force-favicon-refresh).

If you'd rather not assemble the set by hand, [Favikit](https://arnavjhajharia.github.io/favikit/) is a free, MIT-licensed generator ([repo](https://github.com/arnavjhajharia/favikit)) that runs fully in the browser: you drop in one image and it outputs the `.ico`, the PNG sizes, the manifest and the `<head>` tags. Nothing is uploaded.

_Disclosure: this post and Favikit were written with AI assistance._
