# Architecture

## Design Goal

HEMS-Path is intentionally built as a static, single-file web app. The current v4.0 implementation is AW109-specific and does not include a functional airframe selector. The first version avoids React, Vite, Next.js, package managers, databases, authentication, and server-side functions.

This makes the project easy to host on Vercel, easy to inspect in GitHub, and easy for Codex or another AI coding agent to modify in small patches.

## Runtime Flow

1. User opens `index.html`.
2. Leaflet initializes a dark map.
3. User selects origin and destination.
4. The app calculates a geographic midpoint.
5. `runAnalysis()` performs three weather requests:
   - origin
   - midpoint
   - destination
6. Open-Meteo responses are validated.
7. `evaluateMission()` applies the local risk model.
8. UI updates the status box, telemetry cards, rationale table, and briefing strip.

## Important Global State

```js
let map, routeLine;
let markers = { origin: null, destination: null };
let coords = { origin: null, destination: null };
let selectMode = 'origin';
let currentAnalysis = null;
```

Do not wipe `coords` during tab switching, map redraws, or UI-only changes.

## Main Functions

- `initMap()` — initializes Leaflet map and optional geolocation.
- `setSelectMode(mode)` — switches whether the next map click sets origin or destination.
- `setPoint(type, latlng, label)` — stores coordinate and updates marker/input.
- `updateRoute()` — draws the route line when both points exist.
- `fetchWeatherData(lat, lon)` — calls and validates Open-Meteo current weather.
- `runAnalysis()` — coordinates the three-point telemetry request and invokes evaluation.
- `evaluateMission(start, mid, end)` — core risk scoring engine.
- `renderRationaleTable(rows)` — displays the decision rationale.
- `updateBriefingStrip(...)` — displays the dispatch-style summary.
- `copyDispatchLog()` — copies the current analysis to clipboard.
- `downloadStandaloneApp()` — downloads the current HTML document.


## Future Airframe Profile Plan

The current code should continue to behave as a single AW109 prototype until a later airframe-selector patch. A future implementation may introduce a documented `AIRFRAME_PROFILES` concept that keeps profile-specific labels, terminology, performance assumptions, and safety notes together. That future object should remain data-only at first and should not change scoring behavior until profile-specific thresholds are reviewed and intentionally migrated.

Conceptual future fields could include:

- profile identifier and display name
- performance telemetry labels
- RFM/SOP reference text
- profile-specific limitation notes
- reviewed threshold constants, only when approved for that airframe

Do not implement live profile switching in v0.1.x. The selector remains planned for the v0.3.x roadmap.

## Files That Should Usually Change

For small UI/data-source patches:

- `index.html`
- `README.md`
- `docs/*.md`

## Files That Should Usually Not Be Added Early

Avoid these unless a patch explicitly requires them:

- `package.json`
- `node_modules/`
- backend/server files
- authentication configuration
- database migrations
- secret/API key files

## Hosting Architecture

Vercel serves the repository as static files. There is no build command.

```text
Browser -> Vercel static index.html -> CDN resources + Open-Meteo API
```

## Future Architecture Options

Potential future improvements should be phased:

1. Better status/error handling.
2. Better aviation weather source integration.
3. Airframe selector in a later v0.3.x patch after profile assumptions are documented and reviewed.
4. Local saved mission templates.
5. Optional PWA manifest and service worker.
6. Only later: backend, auth, database, or protected API routes.
