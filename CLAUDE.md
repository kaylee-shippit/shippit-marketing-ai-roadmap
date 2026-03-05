# AI Evolution Roadmap

## What this project is

An interactive HTML roadmap board for Shippit's Growth Marketing function. It maps three GTM layers across three sequential phases, with status indicators, placeholder cards, and supporting sections.

The owner is Kaylee Liu (Growth Marketing Manager). It's currently a draft awaiting alignment from Shauna Butcher (Head of Marketing). Placeholder cards are explicitly marked as "shape together" items.

**Live deployment:** https://sparkling-hotteok-9a06de.netlify.app/

## Brand rules

### Colours (mandatory)
- **Purple Heart:** `#6322E5` — primary brand, used for headings, PMM layer, phase tags
- **Deep Teal:** `#003338` — secondary brand, used for Growth layer, dark text
- **White:** `#FFFFFF` — backgrounds, card surfaces
- **Content layer teal:** `#1A6B70` — derived from Deep Teal, lighter shade. NOT Material Design green (#00897B). No green.

### Derived palette (in CSS variables)
```css
--purple: #6322E5;
--purple-light: #F3EEFB;
--purple-mid: #D4B8F9;
--dark: #003338;
--dark-light: #E6EDED;
--pmm: #6322E5;        /* same as purple */
--pmm-bg: #F3EEFB;
--pmm-border: #D4B8F9;
--content: #1A6B70;
--content-bg: #E6F0F0;
--content-border: #8BB5B8;
--growth: #003338;      /* same as dark */
--growth-bg: #E6EDED;
--growth-border: #80A0A4;
```

### Typography
- Font stack: `'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`
- Australian English spelling throughout (e.g. "optimisation" not "optimization", "personalisation" not "personalization")

### Tone
- Concise, clear, and direct. Not corporate or embellished.
- Cards use plain language, not marketing jargon.
- Placeholder cards are honest about what's undefined.

## File structure

```
ai-evolution-roadmap/
  CLAUDE.md          ← this file
  index.html         ← the roadmap (single self-contained HTML file)
```

The roadmap is a **single-file HTML document** — all CSS is inline in a `<style>` block. No external dependencies, no JavaScript, no build step. Just open it in a browser.

## HTML structure

### Main grid (the core of the board)
- CSS Grid: `grid-template-columns: 160px 1fr 1fr 1fr` (label column + 3 phase columns)
- 5 rows: PMM, Content, Growth, Tools & Habits, Outcomes
- Column headers use `.col-header` class (purple background)
- Row labels use `.row-label` class with layer-specific modifiers (`.pmm`, `.content`, `.growth`, `.tools`, `.outcomes`)
- Cells use `.cell` class with layer-specific tint modifiers (`.pmm-cell`, `.content-cell`, etc.)

### Cards
- `.card` — standard card with white background, border, shadow, hover effect
- `.card.placeholder` — dashed border, purple-light background, "Placeholder" badge. These are items to be defined after Shauna alignment.
- `.card-title` — contains a `.status` dot (`.live` green, `.building` orange, `.planned` grey) and the title text
- `.card-body` — muted description text
- `.card-tag` — coloured tag at bottom (`.tag-ai`, `.tag-habit`, `.tag-tool`, `.tag-metric`)

### Below-grid sections
1. **System flow** (`.flow-section`) — horizontal flow diagram showing PMM → AI → Content → AI → Distribution
2. **ABM programs** (`.abm-section`) — 5-column grid of the active ABM programs
3. **Channel outputs** (`.channels-section`) — auto-fill grid of distribution channels
4. **Four focus areas** (`.flow-section`) — 4-column grid showing business focus areas

### Responsive breakpoints
- `1100px` — grid narrows, ABM grid goes to 3 columns
- `768px` — grid goes to 2 columns (label + 1), ABM/channels go to 2 columns

## Key concepts

### Three layers of GTM (Genesys Growth framework)
1. **Research & Positioning (PMM)** — Sofia Nilsson Burston (PMM Lead), Kathy Shi (Sr PMM), Lana Brindley (Technical Content Writer)
2. **Content & Assets** — Content team produces across formats, brand voice
3. **Distribution Engine (Growth)** — Kaylee Liu runs ABM programs, campaigns, paid media

### Three phases (sequential, not date-bound)
1. **Foundations** — Habits first. First AI workflow live.
2. **Content Flywheel** — AI pipeline generating across formats.
3. **Full System** — End-to-end, cross-function, always-on.

### Five ABM programs
1. Trade & Industrial (NowGo)
2. Perishables (NowGo)
3. Bulky & Valuables (Shippit + NowGo)
4. Pipeline Accelerator (Both)
5. Territory Accelerator (Shippit)

### Four business focus areas
1. Land with Enterprise (Retail)
2. Land with Trade
3. Expand with Shipping
4. Expand with B2B

### Card statuses
- **Live** (green dot `#4CAF50`) — already operational
- **Building** (orange dot `#FF9800`) — actively being built now
- **Planned** (grey dot, uses `var(--border)`) — committed but not started
- **Placeholder** (dashed border card) — to be shaped after alignment

## Team roster (for reference)
- **Shauna Butcher** — Head of Marketing
- **Kaylee Liu** — Growth Marketing Manager (owner of this roadmap)
- **Tom Hayward** — Comms
- **Sofia Nilsson Burston** — PMM Lead
- **Kathy Shi** — Senior PMM
- **Lana Brindley** — Technical Content Writer (reports to Sofia)
- **Colin Fung** — Digital Designer
- **Christina Peterson** — Marketing Executive

## Rules for editing

1. **Never fabricate facts or data** about Shippit, its customers, or product features. All facts must be verifiable via shippit.com or support.shippit.com or support.nowgo.io.
2. **No green** — the content layer uses `#1A6B70` (teal derived from brand dark). If adding new colours, derive from the brand palette.
3. **Keep it single-file** — all CSS stays in the `<style>` block. No external files.
4. **Placeholder cards are intentional** — they signal items that need team input. Don't fill them in with made-up content.
5. **Australian English** — "colour" not "color" in copy (CSS properties obviously stay American per spec), "optimisation", "personalisation", "behaviour", etc.
6. **Concise card copy** — each card body should be 1-2 sentences max. If it needs more, it's probably two cards.
