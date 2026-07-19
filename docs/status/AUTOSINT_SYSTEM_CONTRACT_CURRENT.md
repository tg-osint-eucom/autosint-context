<!-- GENERATED FILE: scripts/render_autosint_system_contract.py --write -->
# AUTOSINT System Contract Current

Generated from `config/autosint_system_contract.yml`; do not edit by hand.

## Identity

- Contract version: `autosint-system-contract-v2.1`
- Contract SHA-256: `6ef37a202a8ce88ab9bf6be697c8010415cf5ab1127ece3552b89be756d5c5ef`
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

## Evidence-Backed Theater Closure

TYPED THEATER EVIDENCE CONTRACT
- Closure contract: autosint-theater-closure-v2.1.
- `theater_source_checks` is the cycle-scoped theater evidence collection. It is separate from primary-case `source_checks` and is not subject to the per-case six-row limit.
- Required `theater_source_checks` fields and exact types: source_check_id:string, theater:string, source_family:string, primary_status:string, check_method:string, checked_at:string, window_start:string, window_end:string, current_window:boolean, public_access_mode:string, completion_basis:string, source_urls:array[string], result_summary:string, limitations:array[string], next_check:string.
- Optional source-check fields and exact types: check_method_note:string, adapter_result_ref:string. Source-check `result_summary` and `check_method_note` are informational only and never affect completion.
- `check_method` uses only these exact machine codes: bounded_official_advisory_review, bounded_public_news_review, bounded_multilingual_regional_review, approved_read_only_adapter, not_checked. Generic prose in `check_method` is invalid.
- `public_access_mode` uses only: public_no_login, approved_read_only_adapter, blocked_login_or_license, candidate_only, not_checked.
- `completion_basis` uses only: substantive_content, bounded_no_result, none. Machine-owned primary-status mapping: `Checked and found` -> `substantive_content`; `Checked and not found` -> `bounded_no_result`; `Candidate found, not imported` -> `none`; `Not checked` -> `none`; `Stale` -> `none`; `Blocked / login required` -> `none`. Any other pairing is invalid and is never downgraded.
- Every `source_check_id` and `evidence_refs` item must be an opaque ID matching `^[A-Za-z0-9][A-Za-z0-9:_-]{0,95}$`. URLs, JWTs, signed strings, and values containing `/`, `.`, `?`, `=`, or `@` are invalid IDs.
- Family/method mapping: Official / Advisory -> bounded_official_advisory_review, approved_read_only_adapter; Public News -> bounded_public_news_review, approved_read_only_adapter; Multilingual / Regional -> bounded_multilingual_regional_review, approved_read_only_adapter. `not_checked` is valid only for an honest non-attempt with `primary_status=Not checked` and `public_access_mode=not_checked`; it never counts as a checked attempt or completion. AUTOSINT recomputes `current_window` from timestamps.
- Required theater `family_results` fields and exact types: source_family:string, reported_primary_status:string, reported_coverage_status:string, evidence_refs:array[string], checked_not_found:boolean, follow_up_statuses:array[string], result_summary:string, limitations:array[string], next_check:string.
- Every `family_results` row, including candidate-only, blocked, stale, and honest `Not checked`, must contain at least one `evidence_refs` item naming a `theater_source_checks` row from the same output, theater, and source family. For an honest non-attempt, emit and reference a typed row with `primary_status=Not checked`, `check_method=not_checked`, `public_access_mode=not_checked`, `completion_basis=none`, `checked_at=""`, `current_window=false`, and `source_urls=[]`; it remains incomplete.
- `primary_status` and `reported_primary_status` use only: Checked and found, Checked and not found, Candidate found, not imported, Not checked, Stale, Blocked / login required.
- `reported_coverage_status` uses only: COMPLETE, INCOMPLETE, STALE, UNKNOWN. `follow_up_statuses` items use only: Candidate found, not imported, Blocked / login required, Stale.
- Every `evidence_refs` value names a unique `source_check_id` from the same output, theater, and source family. Only completion evidence must be in the current theater window; stale and candidate follow-up references are allowed and remain incomplete.
- AUTOSINT derives canonical counts, canonical primary status, canonical coverage status, and theater completion from referenced checks. Reported counts and statuses are never authoritative.
- `Checked and found` needs `completion_basis=substantive_content` plus qualifying current evidence with `public_no_login` or a runtime-resolved `approved_read_only_adapter`, and a safe public source URL or trusted adapter result reference.
- `approved_read_only_adapter` is `GATED_DISABLED` for assistant-only evidence unless AUTOSINT resolves `adapter_result_ref` against a trusted runtime record. An absent or untrusted ref never completes coverage.
- `Checked and not found` needs `completion_basis=bounded_no_result`, a referenced current bounded attempt, zero validated found sources, and either a safe public URL identifying the bounded itinerary or a trusted adapter result reference. Its family-result row must also set `checked_not_found=true` and contain `no credible current result was found` in the family `result_summary`; that phrase alone never proves completion.
- Candidate URLs are leads only and use `completion_basis=none`. HTTP availability, source-check summaries, method notes, snippets, titles, blocked pages, and candidate-only rows never prove coverage.
- If positive evidence is unavailable, return an honest incomplete, candidate-only, blocked, stale, or not-checked result. Do not fabricate a case to obtain complete coverage.
- Historical `autosint-system-contract-v2` family results retain their legacy replay shape. Never reinterpret legacy V2 free-text methods or model-reported counts as V2.1 typed evidence.
- V2.1 typed source-check promotion gates: theater_source_check_validation_error_count. These version-specific gates do not alter legacy V2 replay gates.
- Canonical closure-evidence fields: `theater`, `sweep_window_start`, `sweep_window_end`, `minimum_source_families_required`, `minimum_source_families_completed`, `family_results`, `verified_source_count`, `checked_not_found_count`, `candidate_follow_up_count`, `blocked_follow_up_count`, `stale_follow_up_count`, `current_coverage_status`, `theater_verified_complete`, `limitations`, `next_check`, `generated_at`, `source_cycle_id_hash`, `mutation_performed`
- Validation counters: `theater_closure_validation_error_count`, `candidate_as_coverage_error_count`, `minimum_family_gap_count`
- Promotion-blocking closure counters: `theater_closure_validation_error_count`, `candidate_as_coverage_error_count`
- Honest minimum-family gaps block promotion by themselves: `false`
- Legacy v1 closure status: `UNKNOWN`; verified complete: `false`

Candidate, blocked, and stale sources remain visible follow-ups but never count as coverage proof. Legacy v1 rows remain displayable continuity context only; AUTOSINT does not synthesize typed V2.1 evidence from them.

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
