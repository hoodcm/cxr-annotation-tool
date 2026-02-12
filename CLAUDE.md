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
