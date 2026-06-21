# HEMS-Path AW109 Decision Support System

HEMS-Path is a single-file static web app prototype for AW109 helicopter mission risk review. It provides a dark-theme operational risk dashboard using map-selected origin and scene coordinates, browser-side Open-Meteo weather calls, and a local JavaScript risk scoring model.

> **Operational limitation:** This repository is a prototype decision-support aid. It is not a certified aviation weather, dispatch, regulatory, clinical, or operational authority. Validate any use against approved aviation weather sources, local policy, aircraft manuals, and Pilot in Command judgment.

## Current Version

- App: `v4.0`
- Repository package: `v0.1.1-static-deployment-safety`
- Architecture: static HTML/CSS/JavaScript
- Backend: none
- Build system: none
- Hosting target: Vercel static deployment from GitHub

## Repository Structure

```text
hems-path-aw109/
├── index.html
├── README.md
├── vercel.json
├── .gitignore
├── .github/
│   └── pull_request_template.md
└── docs/
    ├── ARCHITECTURE.md
    ├── CODEX_PROMPTS.md
    ├── SAFETY_AND_LIMITATIONS.md
    ├── TESTING.md
    └── ROADMAP.md
```

## How to Run Locally

No installation is required.

1. Download or clone the repository.
2. Open `index.html` in Chrome, Edge, or another modern browser.
3. Select a starting point and scene/arrival point on the map.
4. Click **Run Risk Check**.

## How to Deploy on Vercel

1. Create a new GitHub repository.
2. Upload all files from this package.
3. Go to Vercel and choose **Add New Project**.
4. Import the GitHub repository.
5. Use these settings:

```text
Framework Preset: Other
Root Directory: ./
Build Command: leave blank
Output Directory: ./
Install Command: leave blank
```

6. Deploy.
7. Open the live URL and complete the smoke test in `docs/TESTING.md`.

## External Runtime Dependencies

The app loads these resources from CDNs at runtime:

- Tailwind CSS CDN
- Font Awesome CDN
- Leaflet CSS/JS CDN
- Carto dark map tiles
- Open-Meteo API

This keeps the app simple and portable, but it also means the app requires network access for maps, icons, styling, and weather telemetry.

## Data and Privacy

- No login is used.
- No backend database is used.
- No API keys are stored.
- Mission coordinates are held in browser memory during the session.
- The app calls Open-Meteo with selected latitude/longitude points.

## Codex / AI Coding Workflow

Use one small branch per patch. Do not let an AI coding agent rewrite the full app unless explicitly approved.

Recommended branch naming:

```text
v0.1.2-api-status-polish
v0.2.0-metar-source-research
v0.3.0-airframe-selector
```

Before merging any AI-generated patch, review:

- changed files
- final report
- tests run
- whether mission scoring thresholds changed
- whether backend/auth/API keys/build tools were added unexpectedly

See `docs/CODEX_PROMPTS.md` for ready-to-use prompts.

## Known Limitations

- Ceiling is estimated from cloud cover rather than decoded METAR ceiling.
- Visibility is not currently sourced from an aviation weather endpoint.
- Open-Meteo is not an official aviation briefing source.
- Cat A margin logic is a simplified prototype model and must be validated before any operational use.
- Offline use is limited because CDN dependencies and weather/map calls require network access.

## Suggested Next Patch

`v0.1.2-api-status-polish`

Goal: improve user feedback for API failures, add telemetry timestamps, and make the data source status more explicit without changing the mission scoring logic.
