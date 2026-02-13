# CXR Annotation Tool

## Overview

Browser-based radiology report annotation tool. Pure static SPA — no build step, no server dependencies. Deployed to GitHub Pages.

## Tech Stack

- **UI**: Alpine.js + Tailwind CSS (Play CDN)
- **Storage**: Dexie.js (IndexedDB)
- **CSV**: PapaParse
- **Icons**: Tabler Icons webfont

## Commands

```bash
# Local development
python3 -m http.server 8501

# Open http://localhost:8501
```

## Architecture

```
/                     # Repo root = site root
├── index.html        # Entry point (~2200 lines, Alpine.js app)
├── extraction-format-guide.html  # Import CSV format docs
├── favicon.svg
├── apple-touch-icon.png
├── css/app.css       # Custom styles
├── js/
│   ├── app.js        # Core app logic + Alpine.js component
│   ├── storage.js    # Dexie.js IndexedDB wrapper
│   ├── taxonomy.js   # Finding taxonomy search/matching
│   ├── sentences.js  # Report text parsing
│   ├── actionability.js  # Runtime actionability resolution
│   └── csv-import.js # Extraction CSV import logic
└── data/             # Static JSON (generated externally)
    ├── taxonomy.json
    ├── attributes.json
    ├── actionability-rules.json
    ├── normality-mappings.json
    └── sample-reports.json
```

## Data Update Workflow

The `data/` JSON files are generated from the parent project (`report-labeler-concordance`):

```bash
# From the parent repo
python3 scripts/generate_static_data.py    # writes to ../cxr-annotation-tool/data/

# Then commit here
cd ../cxr-annotation-tool
git add data/ && git commit -m "Update taxonomy data" && git push
```

## Environment Variables

None required. Pure client-side application.

## Project Files

| File | Purpose | Update frequency |
|------|---------|------------------|
| `CLAUDE.md` | Project instructions | As needed |
| `CONTEXT.md` | Stable background reference | Rarely |
| `CHANGELOG.md` | Change history | After substantive changes |
| `TODO.md` | Actionable tasks | Frequently |

## Session Startup

At the start of each session:

1. **Check `TODO.md`** for current tasks and open questions
2. **Read `CONTEXT.md`** for background understanding
3. **Scan recent `CHANGELOG.md`** entries for recent changes

## Session Shutdown

At the end of each session:

1. **Update `TODO.md`** — check off completed items, add new tasks discovered
2. **Update `CHANGELOG.md`** — log substantive changes under `[Unreleased]`

## File Responsibilities

| If you... | Update... |
|-----------|-----------|
| Complete a task | `TODO.md` — check it off |
| Add a new task or question | `TODO.md` — add it |
| Make substantive changes | `CHANGELOG.md` — log under [Unreleased] |
| Learn something that changes understanding | `CONTEXT.md` — update reference |
