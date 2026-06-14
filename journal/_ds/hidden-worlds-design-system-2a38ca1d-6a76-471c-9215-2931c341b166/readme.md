# Hidden Worlds — Design System

> *Every place has a deeper layer — stories, decisions, people, traditions — invisible to most visitors. Hidden Worlds makes it visible.*

This is the brand and product design system for **Hidden Worlds**, the mission behind the world's first **AI travel guide** — free, on WhatsApp, no registration. First deployment: **Dubrovnik Airport (ZLRB)**, Season I · 2026.

Open **`overview.html`** for a visual tour, or the **Design System tab** to browse every specimen, component, and the interactive Travel Guide.

---

## 1. What this system covers

Hidden Worlds operates on **three distinct words, three jobs, no overlap.** Use them consistently:

| Word | Job | What it means |
|---|---|---|
| **Hidden Worlds** | Brand & mission | The world being built. The larger vision. |
| **Travel guide** | The product | The AI on WhatsApp. What the user actually talks to. |
| **Storyhunter** | User identity | What the user *becomes* — someone who finds stories no other tourist does. |

The signature artifact is the **Story Card**: a painted, numbered, take-home trading card (Origin Series, /10). Front = painted artwork + a one-line hook + subject + location + flag. Back = a "Passport Entry" (story name, prose, QR, edition №, archive ID, signature). *Not a souvenir — a conversation starter.*

---

## 2. Sources

Everything here was derived from materials provided in `uploads/`:

- **`hidden-worlds-project-description.md`** — the canonical project description (mission, product, Storyhunter, cards, mechanism, lessons, touchpoints, tone & values). The single source of truth.
- **`Front.png`** — the cover poster: navy field, gold-foil wordmark, "SEASON I · 2026 / DUBROVNIK". Source of the hero treatment.
- **`Frame 73.png`** — a Story Card **front** (Ruđer Bošković): painted oil portrait, season label, Croatian flag, italic hook + small-caps subject.
- **`814aa...png`** — a Story Card **back**: the navy "Passport Entry" layout with logo, QR, prose, signature receipt.
- **`hidden-worlds-white-logo.png`** — the white wordmark lockup (now `assets/logo/hidden-worlds-white.png`).
- **`posters.pdf`** — 10 airport recruitment posters (image-only; could not be rasterized in-tool — they apply the same navy + gold + painted-art system to ZLRB touchpoints).

No codebase or Figma file was provided. Colors and proportions were sampled directly from the poster and card images.

---

## 3. CONTENT FUNDAMENTALS — how Hidden Worlds writes

**Voice in one line:** *a friend, not a service.* Generous, curious, confident. Tells stories rather than reciting facts; asks questions instead of pushing answers.

**Person.** Speaks as **"I"** (the guide) to **"you"** (the Storyhunter). First-person, second-person, conversational. *"I'm your guide here — think local friend, not guidebook."*

**Casing.** Sentence case for everything readable. **Tracked UPPERCASE small-caps** only for labels and ceremony — `SEASON I · 2026`, `DUBROVNIK`, `PASSPORT ENTRY`, category eyebrows. The middot ` · ` is the brand's connective glyph in labels.

**Sentence rhythm.** Short declarative sentences. Direct. Period. Next thought. Then one longer, warmer line for the story. End on action or invitation, **never** on frustration.

**Specifics over generalities.** *"3.1M passengers"* not *"millions."* *"63.5 × 88.9 mm"* not *"trading-card sized."* Real names (Ruđer Bošković, Republic of Ragusa, Gruž, Pile Gate).

**Story-first, gentle.** Lead with a hook that creates curiosity, then reveal a hidden truth that reframes what you thought you knew. Wrong lesson answers get *"most people think this — here's what's actually true"* — never shaming. Right answers celebrate + hand over a usable tip.

**Emoji.** Used **sparingly**, only in the chat/product voice (a 👋 on arrival, a 🎴 when a card is ready). **Never** in brand headlines, on cards, posters, or in formal copy.

**What it is NOT:** not a tour guide reciting history; not a historian or professor; not a generic AI/Google result; not a brochure; not a passenger-management system; not a souvenir shop.

**Sample copy:**
> *"You just landed in Dubrovnik. I'm your guide here — think local friend, not guidebook. 👋 Before you reach the Old Town, want a story most visitors never hear?"*
>
> *"A republic sends its sharpest mind, not its loudest voice."* — card hook
>
> *"The Republic of Ragusa didn't build the largest army. It sent Ruđer Bošković… For a small republic surrounded by empires, brains were the deadliest weapon."* — passport entry

---

## 4. VISUAL FOUNDATIONS

**Overall feel.** Nocturnal, cinematic, collectible. A premium first-edition trading card meets a passport meets a night sky. Warm gold on deep navy, with painted oil artwork as the only imagery.

**Color.** Three families (see `tokens/colors.css`, 150 tokens total):
- **Navy** `#0C1320 → #34467A` — the "night." Page = `--navy-900 #101A2E`; card surfaces = `--navy-850 #142133`; panels = `--navy-750`. Cool, slightly desaturated indigo.
- **Gold** `#9C6E1E → #F2D98F` — the "foil." Brand accent = `--gold-500 #C8943B`. The hero finish is `--gold-foil`, a multi-stop gradient that simulates engraved foil (highlight → mid → deep → catch-light).
- **Cream / parchment** `#FAF6EC → #DCD7C8` — paper & light text. Primary text on navy = `--cream-100 #F4EFE2`. The signature receipt panel is a cooler `--cool-white #F3F4F5`.
- Flag accents (`--flag-red`, `--flag-blue`) appear only on cards. A scoped `--wa-*` set carries the WhatsApp messaging surface (the guide lives there).

**Typography.** A single high-contrast **literary serif** does almost all the work — display, titles, story prose, and tracked small-caps labels — set in **Newsreader** (see substitution note below). Product/chat chrome uses a system **sans** (`--font-ui`); edition numbers and archive IDs use **mono**. Hooks are *italic*. Display is heavy (800), set tight (`-0.012em`); labels are uppercase with `0.22em` tracking.

**Imagery.** Painted **oil-style artwork** — warm, richly colored, candlelit, expressive brushwork — is the brand's only illustration style. Portraits of historical figures, scenes, hidden places. No photography, no flat vector illustration, no stock. Cards are full-bleed art with a dark protection gradient at the bottom for the hook.

**Backgrounds.** Full-bleed navy with a soft radial vignette (`.hw-night`) and an optional faint **gold graticule** — a compass/map grid masked to fade at the edges (`.hw-graticule`). No busy gradients, no purple, no mesh. Texture is subtle (paper grain / engraved lines), never loud.

**Corners & cards.** Generous rounding. The physical Story Card corner is `--radius-card 16px`; back panels are `--radius-lg 20px`; UI cards 14–20px; buttons are full pills (`--radius-pill`). Cards sit on deep, soft shadows (`--shadow-card`) often paired with a 1px **gilt edge** (`--edge-gold`) and a faint inner top-light for convexity.

**Elevation.** On navy, depth = deep diffuse shadow + a faint gold rim, not hard borders. Three steps: `--shadow-panel`, `--shadow-card`, `--shadow-float`. The "foil" affordance adds `--glow-gold`.

**Borders & dividers.** Hairlines are gold at low opacity (`--border-hairline`) or neutral white at 8% (`--border-soft`). The signature divider is a **gilt rule** — a gold gradient fading to transparent at both ends, sometimes with a centered small-caps label.

**Transparency & blur.** Used for overlays (the card-reveal scrim) and the WhatsApp/iOS glass chrome — not as decoration on brand surfaces.

**Motion.** Calm and weighty. Default easing `--ease-out` (cubic-bezier .22,1,.36,1). Reveals fade + rise (`hwCardIn`); the Story Card flips on a slow `--dur-reveal 680ms` 3D rotateY. **No** bounces, no infinite loops on content. Respects `prefers-reduced-motion`.

**Interaction states.** Hover = lift (`translateY(-3px)`) and/or a brighter gold edge/glow; never a color inversion. Press = subtle `scale(0.975)`. Focus = a 3px soft-gold ring. Buttons brighten gold on hover; the primary keeps its foil.

---

## 5. ICONOGRAPHY

Hidden Worlds is **deliberately icon-light.** The brand leans on **type, the wordmark, painted art, and ceremony** rather than a UI icon set. There is no proprietary icon font in the provided materials.

- **Brand marks.** The **wordmark** (`assets/logo/`) is the primary mark — used white on navy, or filled with `--gold-foil` for the hero finish (see the `Logo` component, `variant="foil"`, and the `FoilText` utility). Give it clear space ≥ its cap height.
- **The flag** (Croatian tricolor) is the one recurring iconographic element, top-right on card fronts. The `StoryCard` component renders a stylized tricolor by default; pass `flagSrc` for an exact flag (e.g. a `flag-icons` SVG) when fidelity matters.
- **The QR code** is functional iconography on every card back — links to the full experience.
- **Product/chat UI.** Inside the WhatsApp surface, platform glyphs (📹 📞 😊 📎 send arrow) are used as-is — that's the host platform's vocabulary, not Hidden Worlds'. Small caps "✓ / ✕" mark right/wrong lesson answers.
- **Emoji** appear only in the guide's chat voice, sparingly (👋 🎴). Never on brand surfaces.

**Recommendation / substitution:** If a future product surface needs a UI icon set (settings, nav, etc.), use a **thin-stroke line set** (≈1.5px) to match the refined, literary tone — **Lucide** (CDN: `https://unpkg.com/lucide-static`) is the suggested match. This is a *recommendation*, not an observed asset — confirm with the team before standardizing. Do **not** hand-draw decorative SVG iconography or substitute emoji for icons.

---

## 6. ⚠️ Font substitution — needs confirmation

The real wordmark and card type are set in a **licensed, high-contrast literary serif** (Tiempos / Canela / Lyon class — not provided as files). This system substitutes **Newsreader** (Google Fonts) for display, titles, and story prose. It's a close tonal match (literary, optical sizing, characterful italics) but **not pixel-identical** to the brand face.

- The **logo is shipped as the real artwork** (`assets/logo/`, embedded in the `Logo` component), so the wordmark itself is exact — only set headings/prose use the substitute.
- **Ask:** please send the licensed display + text font files (or confirm Newsreader is acceptable) and we'll swap `tokens/fonts.css` + `--font-display`/`--font-serif`.

Fonts load from the Google Fonts CDN via `tokens/fonts.css` (so `Fonts: none` in the compiler report = no local `@font-face`; this is expected).

---

## 7. Index / manifest

**Root**
- `styles.css` — global entry (import this); `@import`s the four token files + `base.css`.
- `base.css` — brand utilities: `.hw-foil`, `.hw-night`, `.hw-graticule`, `.hw-label`, `.hw-rule`, `.hw-story`.
- `overview.html` — visual tour / cover page (bundle-free).
- `readme.md` — this guide · `SKILL.md` — agent-skill entry point.

**`tokens/`** — `colors.css` (150 tokens · navy/gold/cream + semantic + `--wa-*`), `typography.css`, `spacing.css` (spacing, radii, shadows, motion), `fonts.css`.

**`guidelines/`** — 17 foundation specimen cards (Colors ×5, Type ×5, Spacing ×3, Brand ×4) for the Design System tab.

**`components/`** — 12 React primitives, grouped:
- `core/` — `Button`, `Badge`, `Label`, `Card`, `Input`, `Divider`
- `brand/` — `Logo`, `FoilText`, `StoryCard`
- `guide/` — `ChatBubble`, `LessonChoice`, `StoryMoment`

  Each has `.jsx`, `.d.ts`, `.prompt.md`; each group has one `@dsCard` HTML. Reach components at `window.HiddenWorldsDesignSystem_2a38ca.<Name>` after loading `_ds_bundle.js` (compiler-generated).

**`ui_kits/travel-guide/`** — the product UI kit: an interactive WhatsApp travel-guide phone (`index.html`) composing `ChatScreen` → `LessonFlow` → `Passport` + `CardReveal`, in an iOS frame.

**`assets/`** — `logo/` (white wordmark), `cards/` (Bošković front + back), `brand/` (cover poster).

*Generated by the compiler — never edit: `_ds_bundle.js`, `_ds_manifest.json`, `_adherence.oxlintrc.json`.*
