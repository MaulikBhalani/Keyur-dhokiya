# keyur.framer.website — offline copy

Mirrored on 2026-10-27 with `tools/mirror.py` (run `python3 -I tools/mirror.py site` from the
project root to refresh it). All 34 pages from the site's sitemap are included:

- `index.html` — home. Every other page lives at its own path, e.g. `about/index.html`,
  `work/<slug>/index.html`, `blog/<slug>/index.html`, plus `404/index.html` and a root `404.html`.
- CSS is inlined in each page's `<style>` tags, exactly as Framer ships it.
- `assets/sites/…/*.mjs` — Framer's runtime (React, Motion, the site's components). This drives
  the hover, scroll and appear animations and the client-side page transitions.
- `assets/images/`, `assets/assets/*.woff2`, `assets/third-party-assets/` — images and fonts.
- `assets/cms/` — the project and blog data (Framer CMS records).
- `assets/sites/…/icons/` — the phosphor icon modules the site uses.

## Running it

The JavaScript is loaded as ES modules, which browsers refuse to run from a `file://` URL,
so serve the folder with any static web server. From inside the `site` folder:

    python3 -m http.server 8000

then open http://localhost:8000/. Asset paths are root-absolute (`/assets/...`), so the `site`
folder must be the server's document root. Any static host (Netlify, GitHub Pages, S3, nginx)
works the same way; on hosts that serve `/about` as `about/index.html` directly, no further
configuration is needed.

## Changes from the original

- All `framerusercontent.com` URLs are rewritten to local `/assets/...` paths, and internal
  links to the site are made root-relative.
- The Framer analytics beacon and the Framer editor-bar loader are removed, so pages make no
  network requests.
- The CMS loader was patched to read whole files instead of byte-range queries, so it works on
  a plain static server.
- The "Made in Framer" badge is kept as on the original.
- One decorative SVG (`pGiXYozQ3mE4cilNOItfe2L2fUA.svg`) is missing because the original site
  itself returns 404 for it.
