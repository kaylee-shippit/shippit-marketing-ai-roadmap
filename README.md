# AI Evolution Roadmap

An interactive roadmap board for Shippit's AI Evolution strategy. Maps GTM layers across sequential phases with live status indicators, editable cards, and team collaboration via GitHub.

**Live app:** https://YOUR_USERNAME.github.io/ai-evolution-roadmap/

> Replace `YOUR_USERNAME` with the GitHub username or org after you've set up Pages.

---

## How it works

The roadmap is a single HTML file (`index.html`) with all CSS and JavaScript inline — no build step, no dependencies. Card data lives separately in `data.json` in this repo, which is the single source of truth for the whole team.

When you open the app:
1. It checks whether you have GitHub configured in Settings.
2. If yes, it loads `data.json` directly from this repo via the GitHub API.
3. If no GitHub is configured, it falls back to your browser's localStorage, then to the built-in baseline.

---

## Team setup: GitHub sync

Every team member configures their own browser to load from and save to the shared `data.json`.

### What you need
- The GitHub repo details (owner and repo name — see below)
- A GitHub Personal Access Token (PAT) with the right scope

### Step 1: Create a GitHub PAT

**Option A — Fine-grained PAT (recommended, minimal permissions):**
1. Go to https://github.com/settings/tokens?type=beta
2. Click "Generate new token"
3. Set repository access: "Only select repositories" → choose `ai-evolution-roadmap`
4. Under Permissions, set **Contents** → **Read and write**
5. Leave everything else at "No access"
6. Generate and copy the token

**Option B — Classic PAT:**
1. Go to https://github.com/settings/tokens
2. Click "Generate new token (classic)"
3. Tick the **repo** scope
4. Generate and copy the token

Your PAT is stored only in your own browser's localStorage — it is never transmitted anywhere except directly to the GitHub API.

### Step 2: Configure the app

1. Open the roadmap at https://YOUR_USERNAME.github.io/ai-evolution-roadmap/
2. Click "Settings" (top right)
3. Fill in:
   - **Owner / org:** your GitHub username or org
   - **Repo name:** `ai-evolution-roadmap`
   - **Personal access token:** paste your PAT
   - **Branch:** `main`
4. Click "Save settings" — the app loads from GitHub immediately

### Step 3: Edit and save

- Click "Edit" to enter edit mode (drag cards, add/edit/delete cards)
- Click "Save" to push your changes to `data.json` in the repo
- The status bar shows save progress and confirmation

### Collaboration model

- `data.json` in this repo is the single source of truth
- Saves are last-write-wins — if two people save simultaneously, the second gets a SHA mismatch error. Fix: reload the page → re-apply your change → save again
- Each person uses their own PAT — never share tokens between people

---

## ClickUp export

When you're ready to ship work to ClickUp, use the built-in export.

1. Click "Export to ClickUp" (top right)
2. Choose a tab:

**Tab 1 — Copy as text:** Copies a structured plain-text task list to your clipboard for manual paste into ClickUp, Notion, or Slack.

**Tab 2 — Push via API:** Pushes all cards directly to a ClickUp list as tasks. You'll need:
- A ClickUp API token: https://app.clickup.com/settings/apps → "API Token" → "Generate"
- A ClickUp List ID: open the target list in ClickUp, the URL contains `/list/901XXXXXXXXX` — copy that numeric ID

> Note: the API push is additive — running it twice creates duplicate tasks. Use it once per milestone, not as a recurring sync.

---

## File structure

```
ai-evolution-roadmap/
  index.html    — the app (self-contained, all CSS/JS inline)
  data.json     — shared card data (edited via app, saved via GitHub API)
  README.md     — this file
  CLAUDE.md     — brand rules and architecture notes for Claude Code sessions
  .gitignore    — excludes macOS and editor artefacts
```

---

## Local development

No build step required. Open directly in a browser:

```bash
open index.html
```

Or serve locally to avoid any fetch restrictions:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## Updating the roadmap

Card data lives entirely in `data.json`. To update it:

1. Open the live GitHub Pages URL
2. Configure Settings with your PAT (first time only — browser remembers it)
3. Click "Edit" and make changes
4. Click "Save" — commits `data.json` directly to `main`

For structural changes to the app itself (`index.html`), use a branch and PR if you want review before it goes live.
