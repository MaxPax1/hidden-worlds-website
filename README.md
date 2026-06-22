# Hidden Worlds — landing page

Two builds of the same landing page live here:

## Repo root — the static site (preview)
Self-contained, client-rendered page (design-system runtime resolves the
components in the browser). This is what GitHub Pages serves, straight from the
repo root.

- **Live preview:** https://maxpax1.github.io/hidden-worlds-website/
- **Pages setting:** repo **Settings → Pages → Source: Deploy from branch →
  `main` / `/ (root)`**. (`.nojekyll` is included so the underscore-prefixed
  `_ds/` runtime is served.)
- Files: `index.html` (`/`) and `story-card.html`. WhatsApp links resolve at
  runtime from the design-tool `whatsappUrl` prop (defaults to the real number).

## `fastapi-build/` — the hosting build (hand this to the team)
The page **prepared for the Hidden Worlds FastAPI/forge service** — `templates/`
+ `static/`, with the `{{ }}` tokens removed, asset paths rewired to `/static/`,
and links pointing at routes. **See [`fastapi-build/INTEGRATION.md`](fastapi-build/INTEGRATION.md)**
for install steps and the one route to add (`GET /story-card`).

This is the version to deploy. The static site at the repo root is just the
preview / source of the design.

---

### Notes
- WhatsApp number: `wa.me/385998427803` (search/replace to change).
- Legal notice under every WhatsApp CTA opens a Terms/Privacy modal that iframes
  `https://hiddenworlds.travel/terms`.
- `fastapi-build/` is derived from the root static site (token removal, `/static/` paths,
  dead-code/asset pruning); regenerate it if `docs/` changes. The exact
  transforms are documented in `fastapi-build/INTEGRATION.md`.
