# Codex Prompt Templates

Use these prompts one patch at a time. Paste the prompt into Codex after the repository exists in GitHub.

## Prompt 1 — API Status and Timestamp Polish

```text
Implement v0.1.2 — API Status and Timestamp Polish

Repository:
[PASTE GITHUB REPO URL]

Current app status:
Static single-file HEMS-Path AW109 app deployed from index.html. It uses browser-side Open-Meteo calls, Leaflet, Tailwind CDN, and Font Awesome CDN. No backend and no build system.

Goal:
Improve weather data transparency without changing mission scoring logic.

Scope:
This patch should only do:
- Display the Open-Meteo poll time in the main telemetry/status area.
- Show clear labels for Base, Midpoint, and Scene weather source status.
- Preserve existing risk scoring thresholds exactly.
- Improve user-facing COMM_FAILURE details if one of the three nodes fails.

Do not:
- rewrite the app
- change evaluateMission scoring logic
- add backend/auth/API keys
- add React/Vite/Next/package.json
- remove single-file portability
- use alert(), confirm(), or prompt()

Likely files to change:
- index.html
- README.md
- docs/TESTING.md

Testing:
- Open index.html locally
- Select origin and destination
- Run Risk Check
- Confirm source statuses and timestamp display
- Confirm Green/Yellow/Red behavior remains unchanged
- Confirm no blocking alert boxes
- git diff --check
- git diff --name-only HEAD~1 HEAD

Branch:
v0.1.2-api-status-polish

Commit message:
v0.1.2 add telemetry source status

Final report:
- files changed
- branch name
- commit hash
- tests run
- confirmation that mission scoring logic was unchanged
- confirmation that no backend/auth/API keys/build tools were added
```

## Prompt 2 — Add Airframe Selector

```text
Implement v0.3.0 — Airframe Selector Prototype

Repository:
[PASTE GITHUB REPO URL]

Goal:
Add an airframe selector while preserving current AW109 behavior as the default.

Scope:
This patch should only do:
- Add an airframe selector to the existing controls.
- Keep AW109 as the default profile.
- Add EC135 and Bell 407 prototype profiles as clearly labeled prototype values.
- For Bell 407, change Cat A terminology to Power Margin Reserve in the UI when selected.
- Keep existing AW109 scoring behavior unchanged when AW109 is selected.

Do not:
- change AW109 thresholds
- add backend/auth/API keys
- rewrite the UI
- add package.json or build tooling
- remove safety disclaimers

Testing:
- Confirm AW109 default outputs match pre-patch behavior for the same inputs
- Confirm EC135 selector changes the displayed profile
- Confirm Bell 407 selector changes Cat A label terminology
- Confirm no console errors
- git diff --check

Branch:
v0.3.0-airframe-selector

Commit message:
v0.3.0 add airframe selector prototype
```

## Prompt 3 — METAR/TAF Research Stub

```text
Implement v0.2.0 — Aviation Weather Source Research Stub

Repository:
[PASTE GITHUB REPO URL]

Goal:
Prepare the app for future METAR/TAF integration without replacing Open-Meteo yet.

Scope:
This patch should only do:
- Add documentation in docs/ about candidate aviation weather data sources.
- Add a clearly named placeholder function for future METAR parsing.
- Do not call any new API yet.
- Do not change current Open-Meteo behavior.
- Add UI copy that says ceiling is currently estimated from cloud cover.

Do not:
- add API keys
- add backend
- add paid service dependencies
- change risk scoring
- remove Open-Meteo fallback

Testing:
- Confirm app behavior is unchanged
- Confirm new documentation is present
- Confirm UI limitation copy is visible
- git diff --check

Branch:
v0.2.0-aviation-weather-research-stub

Commit message:
v0.2.0 document aviation weather integration path
```
