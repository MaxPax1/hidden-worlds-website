# Hidden Worlds — site handoff for deployment

Static marketing site for Hidden Worlds. Goal: serve it from our real domain on company hosting.

## TL;DR

Fully static. No backend, no build step. Serve these from the web root over HTTPS:

- `index.html` — the page
- `support.js` — page logic (referenced by `index.html`)
- `assets/` — images
- `_ds/` — design-system runtime + tokens/CSS (**must be served, underscore prefix and all**)

That's the entire live site. Everything else in the repo (`journal/`, `refined/`) is old drafts and is **not** part of the live site — ignore or delete.

## Things that aren't obvious

1. **Client-side rendering layer.** `index.html` uses `<x-import component-from-global-scope=...>` custom elements and `{{ waUrl }}` / `{{ requestUrl }}` bindings. These are resolved **in the browser** by `_ds/.../_ds_bundle.js` at runtime. Implications:
   - Must be served over HTTP(S). Opening `index.html` as a `file://` will not render correctly.
   - The `_ds/` directory must be publicly reachable, including the underscore-prefixed path. (Any host that hides `_`-prefixed dirs by default — e.g. Jekyll — will break it. That's what the `.nojekyll` file was for on GitHub Pages; harmless elsewhere.)
   - Serve `.js` and `.css` with correct MIME types (any normal static host does this).

2. **WhatsApp link.** The CTA buttons point at a WhatsApp number that currently defaults to `https://wa.me/385997890123` (see `index.html`, `const waUrl = ...`). **Confirm or replace with the real production number before go-live.**

3. Single page, no client-side routing — no SPA rewrite rules needed.

## Suggested deploy

Drop the four items above on whatever static hosting we use (S3+CloudFront, Nginx, Netlify, Cloudflare Pages, etc.), point the domain at it, enable HTTPS. No env vars, no secrets.

Repo: https://github.com/MaxPax1/hidden-worlds-website
