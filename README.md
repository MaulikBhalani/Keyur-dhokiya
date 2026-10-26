# keyur.framer.website — offline copy

Mirrored on 2026-10-27 with `tools/mirror.py`. All 34 pages from the site's sitemap are included.

This build is made for **https://maulikbhalani.github.io/Keyur-dhokiya/**: every asset path,
internal link and router route starts with `/Keyur-dhokiya`. To rebuild for a different location,
run from the project root:

    python3 -I tools/mirror.py site /Keyur-dhokiya     # GitHub Pages project site (current build)
    python3 -I tools/mirror.py site                    # a domain root, e.g. a custom domain or localhost:8000/

After redeploying, do a hard refresh (Cmd+Shift+R) once: the JavaScript files keep the same names
between builds, so the browser and GitHub's CDN may serve the previous build's copies for up to
10 minutes, which makes page-to-page navigation request the old asset paths.

Contents:

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
so it needs a static web server. Because this build's paths start with `/Keyur-dhokiya`, a local
server must expose the folder under that same path. From the project root:

    mkdir -p /tmp/pages && ln -sfn "$PWD/site" /tmp/pages/Keyur-dhokiya
    python3 -m http.server 8000 --directory /tmp/pages

then open http://localhost:8000/Keyur-dhokiya/. (A build made without a base path can be served
straight from the `site` folder at http://localhost:8000/.)

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
