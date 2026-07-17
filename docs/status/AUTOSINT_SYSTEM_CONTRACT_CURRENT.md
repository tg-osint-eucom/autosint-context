<!-- GENERATED FILE: scripts/render_autosint_system_contract.py --write -->
# AUTOSINT System Contract Current

Generated from `config/autosint_system_contract.yml`; do not edit by hand.

## Identity

- Contract version: `autosint-system-contract-v1`
- Contract SHA-256: `d9370a4eee824686cac62021a67c04fdc7a9e1b1261535d6c4a21ee4e0f2000d`
- Policy owner: `config/autosint_system_contract.yml`

## External Scout

- Producer mode: `scout_findings_normalized`
- Direct strict packets: `fallback_only`
- Primary transport: `inline_fenced_json`
- Fallback transport: `downloadable_json_attachment`
- Never emit both full payloads: `true`
- Natural cases: `1-3`; absolute maximum `5`
- Bounded recovery: exactly `1` case
- Cycle aggregate binding: `primary_case_only`

ChatGPT produces Scout Findings. AUTOSINT deterministically normalizes them into strict candidate packets. Direct `candidate_packets` is fallback-only.

## Theater And Lane Policy

- Required theaters (7): `SOCCENT`, `SOCEUR`, `SOCPAC`, `SOCAFRICA`, `SOCSOUTH`, `SOCKOR`, `SOCOMD`
- Natural cycle scope: `GLOBAL_THEATER_SWEEP`; recovery scope: `FOCUSED_THEATER_DEEP_DIVE`
- Deep-dive rotation: one mandatory oldest-due slot per successful global cycle; every theater due within `7` successful cycles
- Deep-dive capacity: `1` rotation + `1` distinct priority + up to `1` severe slot
- Operational lanes: `19`

- `official_advisory`: Official / Advisory
- `public_news`: Public News / Wires / Trade Press
- `multilingual_regional`: Multilingual / Regional
- `social_osint`: Social OSINT / Public Reaction
- `traffic_movement`: Traffic / Movement
- `satellite_geospatial`: Satellite / Geospatial
- `weather_environment`: Weather / Environment
- `prediction_polymarket`: Polymarket
- `prediction_kalshi`: Kalshi
- `prediction_other`: Manifold / Other Prediction Markets
- `broad_market`: Broad Market
- `oil_energy`: Oil / Energy
- `shipping_tanker`: Shipping / Tanker
- `insurance_freight_rates`: Insurance / Freight / Rates
- `defense_large_cap`: Defense Large-Cap
- `defense_mid_small`: Defense Mid/Small
- `regional_markets`: Regional Markets
- `crypto_risk`: Crypto / Risk
- `public_comments`: Public Comments / Reaction

Required prediction rows include `other_prediction_markets` (Manifold / Other Prediction Markets). Required market/finance rows include `insurance_freight_rates`.
Required semantic row fields: `status`, `summary`, `source_urls`, `metrics`, `what_it_suggests`, `what_it_does_not_prove`, `collection_gap`, `next_check`, `cue_only`, `collection_complete`.

## Model Policy

- Required label: `GPT-5.6 Sol Pro`
- Selection status: `OPERATOR_CONFIRMED`
- Account-setting machine verification: `NOT_PERFORMED`
- Cycle attribution: `RECEIPT_REQUIRED`
- API model id: `NOT_INFERRED`

The Project selection is operator-confirmed. Cycle attribution still requires a receipt field; this is not an API migration claim.

## Proof Policy

- Target: `3` consecutive eligible natural cycles
- Manual recovery counts: `false`
- Direct capture counts: `false`
- Minimum active threads: `1`
- Health RED allowed: `false`

## Navigation And RFI

- Overview: `/rfi` and `/api/v1/rfi`
- Workspace preview: `/rfi/{workspace}` and `/api/v1/rfi/{workspace}`
- RFI is read-only, analyst-review-only, candidate-input-only, not Evidence, not OSIR, not apply/import, and not commander-ready.

## Capability Truth

- `ABSENT`
- `DOCUMENTED_ONLY`
- `PARTIAL`
- `IMPLEMENTED_UNTESTED`
- `IMPLEMENTED_TESTED`
- `OPERATIONALLY_PROVEN`
- `APP_INTEGRATED`
- `DEGRADED`
- `GATED_DISABLED`
- `LEGACY_REMOVED`
- `NOT_APPLICABLE`
- `UNVERIFIED`

Bare `IMPLEMENTED`, `COMPLETE`, and `DONE` statuses are forbidden.

## Degraded Behavior

- API remains read-only under contract RED: `true`
- Operator label under RED: `CONTRACT_CONFLICT_RED`
- Scheduled prompt blocked under RED: `true`
- Scheduled harvester blocked under RED: `true`
- WARN blocks runtime: `false`

## Safety Boundary

- Candidate input only: `true`
- Commander ready: `false`
- Mutation performed: `false`
- Private browser state read: `false`
- DB mutation: `false`
- Evidence mutation: `false`
- Case-link mutation: `false`
- OSIR/apply/import: `false`
