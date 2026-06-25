# FastAPI integration — Hidden Worlds landing

This folder is the landing page prepared for the Hidden Worlds FastAPI/forge
service. It is `templates/` + `static/`, with the design-tool `{{ }}` tokens
removed, asset paths rewired to `/static/`, and internal links pointing at routes.

## Files

```
templates/
  index.html          ->  the homepage
  story-card.html     ->  the Story Card detail page
  terms-viewer.html   ->  homepage with the Terms & Privacy modal already open
static/
  support.js          ->  design-system runtime
  _ds/...             ->  design-system bundle + tokens
  assets/...          ->  images
```

## Static mount

Serve the `static/` folder at `/static` (the templates reference
`/static/support.js`, `/static/_ds/...`, `/static/assets/...`).

```python
from fastapi.staticfiles import StaticFiles
app.mount("/static", StaticFiles(directory="static"), name="static")
```

## Routes to add

Three HTML routes, each returning the matching template:

| Route                | Template               | Purpose                                            |
|----------------------|------------------------|----------------------------------------------------|
| `GET /`              | `index.html`           | Homepage                                           |
| `GET /story-card`    | `story-card.html`      | Story Card detail page                            |
| `GET /terms-viewer`  | `terms-viewer.html`    | Homepage with the legal modal open (see below)    |

```python
from fastapi import Request
from fastapi.responses import HTMLResponse
from fastapi.templating import Jinja2Templates

templates = Jinja2Templates(directory="templates")

@app.get("/", response_class=HTMLResponse)
async def home(request: Request):
    return templates.TemplateResponse("index.html", {"request": request})

@app.get("/story-card", response_class=HTMLResponse)
async def story_card(request: Request):
    return templates.TemplateResponse("story-card.html", {"request": request})

@app.get("/terms-viewer", response_class=HTMLResponse)
async def terms_viewer(request: Request):
    return templates.TemplateResponse("terms-viewer.html", {"request": request})
```

The templates have **no remaining `{{ }}` tokens**, so they can also be served as
plain static HTML if you prefer — no template context is required.

## About `/terms-viewer` (the new page)

This is a standalone copy of the homepage that opens the **Terms & Privacy modal
from first paint** and keeps it open through the page's client-side render cycle.
It exists so an **outside link can deep-link straight into the legal text** — the
visitor lands on the live, colorful homepage with the terms already open over it,
and closing the modal drops them onto the homepage to explore.

- Default opens the Terms section. `GET /terms-viewer?tc=privacy` opens straight
  to the Privacy section.
- The modal iframes `https://hiddenworlds.travel/terms` (the raw legal page,
  served elsewhere) — that page is unchanged and still serves as the source.
- The **WhatsApp onboarding link** (the "By continuing, you agree to..." line)
  should point at `https://hiddenworlds.travel/terms-viewer`.

## Notes

- WhatsApp number: `wa.me/385998427803` (search/replace to change).
- `fastapi-build/` is derived from the root static site (token removal,
  `/static/` paths, dead-code/asset pruning). If the root site changes,
  regenerate this folder with the same transforms.
