# Hidden Worlds landing page — FastAPI/forge integration

This folder is the landing page **prepared for the Hidden Worlds FastAPI service**
(the `landing_page.zip` structure). It mirrors that layout exactly:

```
templates/
  index.html         → GET /
  story-card.html    → GET /story-card   (NEW route, see below)
static/
  support.js
  _ds/...            (design-system runtime + tokens/css)
  assets/...         (only the 9 images the pages actually use)
```

## How to install
1. Copy `templates/*` into the service's `templates/`.
2. Copy `static/*` into the service's `static/` (nginx serves `/static` from
   `/var/www/assets/static`; `runner.py` copies `static/` there on startup, so this
   just merges in).
3. **Add one route:** `GET /story-card` → `templates/story-card.html`.
   (`GET /` and `GET /terms` already exist.) The homepage links to `/story-card`
   in three places and the sub-page links back to `/`.

## Serving note (important)
These pages are **client-rendered** by the design-system runtime (`support.js` +
`_ds/_ds_bundle.js` resolve `<x-dc>` / `<x-import>` components in the browser).
They need **no server-side templating** — serve them as plain files (e.g.
`FileResponse`).

If you serve them through `Jinja2Templates` instead, that's also fine now: the
dc-runtime `{{ waUrl }}` / `{{ requestUrl }}` tokens that would have collided with
Jinja have been **removed** (replaced with the real `wa.me` URL), and there are no
other `{{ }}`, `{% %}`, or `{# #}` tokens. No template context is required.

## What was changed vs. the static GitHub Pages version
- All asset paths rewired from relative (`assets/`, `_ds/`, `./support.js`) to
  absolute `/static/...`.
- dc-runtime URL tokens hard-coded to the real number:
  **`https://wa.me/385998427803`** (5 links total: 4 "Start Storyhunting" +
  1 "Request your city" which appends a prefilled `?text=`). To change the number,
  search/replace `wa.me/385998427803` in both templates.
- Cross-page links point at the routes `/` and `/story-card`.
- Dropped 4 unused hero images (~28 MB of dead `heroMap` code) and the dead
  `heroBgStyle` logic.

## External dependencies (CSP / network)
- **Fonts:** Newsreader loads from Google Fonts CDN
  (`fonts.googleapis.com` + `fonts.gstatic.com`). Allow these if a CSP is set.
- **Terms & Privacy modal:** the legal notice under every WhatsApp button opens a
  modal that **iframes `https://hiddenworlds.travel/terms`** (`#terms` / `#privacy`).
  That page must permit framing (X-Frame-Options / CSP `frame-ancestors`). The
  existing site already iframes it, so this should already be allowed — worth a
  quick confirm.

## Still open (product decision, not a blocker)
- The sticky **nav button** also opens WhatsApp but does **not** carry the legal
  notice (a legal sentence in the header reads broken, esp. mobile). The four
  primary in-body CTAs all carry it. Decide whether the nav needs it too.
