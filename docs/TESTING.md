# Testing

## Local Smoke Test

Before deploying or merging a PR:

1. Open `index.html` locally in Chrome or Edge.
2. Confirm the dashboard renders.
3. Confirm the prototype disclaimer is visible.
4. Confirm `AW109` or `Current Airframe: AW109` is visible before running analysis.
5. Confirm the telemetry panel is labeled as AW109-specific performance telemetry.
6. Confirm the Open-Meteo poll time area is visible and starts in a pending/standby state.
7. Confirm Base Source, Midpoint Source, and Scene Source labels are visible.
8. Confirm the map renders.
9. Click the origin box and select a map point.
10. Click the destination box and select a second map point.
11. Click **Run Risk Check**.
12. Confirm one of these occurs:
   - Green/Yellow/Red decision displays, or
   - clean COMM_FAILURE message displays without a crash.
13. Confirm the poll timestamp updates after the risk check.
14. Confirm Base/Midpoint/Scene source statuses show `OPEN-METEO OK` or a clear node-specific failure.
15. Open browser developer console and check for unexpected errors.
16. Click **Copy Standard Briefing Log** after a successful run.
17. Confirm inline copy status appears and no blocking alert appears.
18. Click each tab and confirm coordinates/markers are not wiped.

## Vercel Smoke Test

After deployment:

1. Open the Vercel URL.
2. Repeat the local smoke test.
3. Confirm the page is served over HTTPS.
4. Confirm clipboard behavior works on the live URL.
5. Confirm mobile layout on a phone-width viewport.

## Manual Regression Checklist for AI Patches

- [ ] AW109-specific labeling visible before analysis
- [ ] AW109-specific performance telemetry label visible
- [ ] Future-airframes note visible without a functional selector
- [ ] Open-Meteo poll timestamp visible and updated after analysis
- [ ] Base/Midpoint/Scene source statuses visible
- [ ] COMM_FAILURE identifies failed weather node(s) where possible
- [ ] Mission risk thresholds unchanged unless intended
- [ ] No backend added
- [ ] No auth added
- [ ] No API keys added
- [ ] No package manager added
- [ ] Static hosting still works
- [ ] Disclaimer remains visible
- [ ] PIC authority language remains visible
- [ ] Map marker state persists across tab switches
- [ ] COMM_FAILURE is clear and non-crashing

## Suggested Test Scenarios

### Scenario 1: Normal Corridor

- Select two nearby points in a fair-weather region.
- Expected: app returns a decision and rationale table.

### Scenario 2: Missing Destination

- Select only origin.
- Click Run Risk Check.
- Expected: non-blocking INPUT REQUIRED status.

### Scenario 3: Network/API Failure

- Disable network or block Open-Meteo.
- Click Run Risk Check.
- Expected: COMM_FAILURE status, no crash.

### Scenario 4: Clipboard Without Analysis

- Load app fresh.
- Click Copy Standard Briefing Log.
- Expected: inline warning to run risk check first.
