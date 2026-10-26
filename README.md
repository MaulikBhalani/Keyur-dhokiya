# keyur.framer.website — offline copy

Mirrored on 2026-10-27. Everything the page needs is in this folder:

- `index.html` — the page, with all CSS inlined (Framer ships styles inside `<style>` tags).
- `assets/sites/…/*.mjs` — Framer's runtime (React, Motion, the site's components). This is what drives hover, scroll and appear animations.
- `assets/images/`, `assets/assets/*.woff2`, `assets/third-party-assets/` — images and fonts.
- `assets/cms/` — the project list data (Framer CMS records).
- `assets/sites/…/icons/` — the phosphor icon modules the page uses.

## Running it

The JavaScript is loaded as ES modules, which browsers refuse to run from a `file://` URL.
Serve the folder with any static web server, for example:

    python3 -m http.server 8000

then open http://localhost:8000/. Any static host (Netlify, GitHub Pages, S3, nginx) works too.

## Changes from the original

- All `framerusercontent.com` URLs are rewritten to local relative paths.
- The Framer analytics beacon and the Framer editor-bar loader are removed, so the page makes no network requests.
- The CMS loader was patched to read whole files instead of byte-range queries, so it works on a plain static server.
- The "Made in Framer" badge is still present; delete the `<a class="… __framer-badge">` element in `index.html` to remove it.
- One decorative SVG (`pGiXYozQ3mE4cilNOItfe2L2fUA.svg`) is missing because the original site itself returns 404 for it.
