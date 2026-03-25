# AI Evolution Roadmap

## What this project is

An interactive HTML roadmap board for Shippit's Growth Marketing function. It maps three GTM layers across three sequential phases, with status indicators, placeholder cards, and supporting sections.

The owner is Kaylee Liu (Growth Marketing Manager). It's currently a draft awaiting alignment from Shauna Butcher (Head of Marketing). Placeholder cards are explicitly marked as "shape together" items.

**Live deployment:** https://kaylee-shippit.github.io/shippit-marketing-ai-roadmap

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
  index.html         ← the interactive roadmap board (HTML + CSS + JS, all inline)
  data.json          ← card state; read/written via GitHub API for shared collaboration
```

The roadmap is a **two-file project**:
- `index.html` — all HTML, CSS, and JavaScript inline. Open directly in a browser with no build step or server.
- `data.json` — the card data store. On page load the board fetches this from GitHub and renders from it. On save it writes back. Falls back to the hardcoded `DEFAULT_DATA` baseline in the JS if GitHub is not configured.

## Interactive features

### Edit mode
- **✏️ Edit** button in the header toggles edit mode. Controls are hidden by default for clean presentation.
- In edit mode: hover a card to reveal pencil (edit) and × (delete) buttons. Double-click a card to open the edit modal.

### Edit modal
Fields: Title, Description, Status (live / building / planned / none), Tag, Assignee (dropdown from team roster), Placeholder toggle.

### Drag and drop
Cards are draggable across any cell in edit mode. Uses the native HTML5 Drag and Drop API — no external library.

### Assignee chips
Cards display a coloured avatar + name at the bottom when an assignee is set.

### Add / delete cards
- **+ Add card** button appears at the bottom of each cell in edit mode.
- **×** on card hover deletes with a confirmation prompt.

### GitHub sync
- **💾 Save** pushes `data.json` to the configured GitHub repo via the Contents API. Each save creates a commit (free version history).
- **⚙ Settings** panel — paste GitHub owner, repo, PAT, and branch once. Stored in `localStorage` per device, never committed to the repo.
- On page load, the board auto-fetches the latest `data.json` from GitHub so everyone sees current state.

### ClickUp export
- **↗ Export to ClickUp** — copy as structured text (always available) or push cards directly to a ClickUp list via the REST API (requires a ClickUp API token and List ID).

### Password gate
- On page load, a full-screen gate prompts for the team password (`Shippit2026`). Auth is verified via SHA-256 and persisted in `sessionStorage` — the gate doesn't reappear until the browser tab is closed.

### View toggle
- **By workstream / By due date** toggle above the phase grid. Workstream view shows the swimlane hierarchy (parent + children). Date view flattens all cards sorted by due date, with a workstream label on child cards.

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
1. **ClickUp connective tissue strip** (`.clickup-tissue`) — horizontal flow showing how tasks move from research to distribution via ClickUp automation
2. **Endgame diagram** (`.endgame-section`) — three-layer system diagram (Research → Content → Distribution) with SVG concentric circle, tool pills, workflow flows, and a 30-day PoC callout

### Responsive breakpoints
- `1100px` — grid narrows
- `768px` — grid goes to 2 columns (label + 1)

## Key concepts

### Three layers of GTM (Genesys Growth framework)
1. **Research & Positioning (PMM)** — Sofia Nilsson Burston (PMM Lead), Kathy Shi (Sr PMM), Lana Brindley (Technical Content Writer)
2. **Content & Assets** — Content team produces across formats, brand voice
3. **Distribution Engine (Growth)** — Kaylee Liu runs ABM programs, campaigns, paid media

### Three phases (sequential, not date-bound)
1. **Foundations** — Habits first. First AI workflow live.
2. **Content Flywheel** — AI pipeline generating across formats.
3. **Full System** — End-to-end, cross-function, always-on.

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
3. **Two files only** — `index.html` (all CSS and JS inline) and `data.json` (card state). No other files, no external dependencies, no build step.
4. **Placeholder cards are intentional** — they signal items that need team input. Don't fill them in with made-up content.
5. **Australian English** — "colour" not "color" in copy (CSS properties obviously stay American per spec), "optimisation", "personalisation", "behaviour", etc.
6. **Concise card copy** — each card body should be 1-2 sentences max. If it needs more, it's probably two cards.
