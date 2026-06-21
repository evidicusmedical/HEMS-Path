# Safety and Limitations

## Required Disclaimer

HEMS-Path is a prototype decision-support aid. It is not a certified aviation weather, dispatch, regulatory, clinical, or operational authority. Validate any use against approved aviation weather sources, local policy, aircraft manuals, and Pilot in Command judgment.

## Operational Boundaries

Do not use this app as the sole basis for flight, dispatch, patient care, or regulatory decisions.

## Current Data Source Limitations

- Weather data comes from Open-Meteo.
- Open-Meteo is not presented here as an official aviation briefing authority.
- Ceiling is estimated from cloud cover by a local helper function.
- Visibility is not yet directly integrated from an aviation weather source.
- METAR/TAF parsing is not yet implemented.

## Current Performance Model Limitations

- Density altitude and Cat A reserve calculations are simplified prototype logic.
- Airframe thresholds should be validated against aircraft manuals and local SOPs.
- Terrain mode is manually selected and not derived from a terrain database.
- Mountain wave, obscuration, freezing precipitation, and other hazards need stronger data support before operational reliance.

## UI Safety Rules

- Do not use `alert()`, `confirm()`, or `prompt()` because blocking dialogs can interrupt workflow.
- Use inline warnings and status areas.
- Preserve coordinates when switching tabs or interacting with non-map UI.
- Do not hide data-source limitations.
- Keep the PIC authority disclaimer visible.

## AI Coding Safety Rules

Every Codex patch must state whether it changes mission scoring logic.

Patches that change thresholds, regulatory references, airframe performance, or safety labels require manual review before merge.
