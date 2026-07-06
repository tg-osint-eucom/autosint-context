# AUTOSINT Sensor Coverage Requirements Trace

This trace converts the Case Threads buyer/operator questions into concrete requirements for global sensor coverage and regional case discovery.

Inputs:

- `docs/product/AUTOSINT_CASE_THREADS_BUYER_QUESTIONS.md`
- `docs/product/AUTOSINT_CASE_THREADS_DESIGN_V1.md`
- `docs/product/AUTOSINT_LIVE_CASE_BOARD_ACCEPTANCE_TRACE.md`
- `docs/AUTOSINT_GLOBAL_SENSOR_COVERAGE_POLICY.md`
- `docs/AUTOSINT_THEATER_WATCH_POLICY.md`

Safety boundary: requirements tracking is read-only. It does not mutate DB, raw Evidence, case links, source config, OSIR, apply/import paths, launchd, or commander-ready state.

## Trace Table

| Requirement ID | Question/category | Current answer | Status | Evidence file/module | Next action/workstream |
|---|---|---|---|---|---|
| SCOV-001 | Case/thread identity | Stable `thread_id`, `topic_key`, workspace, display title, current packet, and lineage are implemented. | Implemented | `core/external_scout_threads.py`; `docs/product/AUTOSINT_CASE_THREADS_DESIGN_V1.md` | Keep alias and split/merge tests current. |
| SCOV-002 | Topic normalization | Deterministic topic key and known alias map exist for current major topics. | Implemented | `core/external_scout_threads.py` | Expand aliases as new regions appear. |
| SCOV-003 | Append/update | Valid packets append to thread timelines; duplicates are skipped; lower-quality packets can append without replacing best current state. | Implemented | `core/external_scout_threads.py`; `tests/test_external_scout_threads.py` | Continue regression tests when prompt schema changes. |
| SCOV-004 | Freshness/staleness | 90-minute freshness plus current/stale/archive retention is implemented. | Implemented | `core/external_scout_threads.py`; `/external-scout/threads` | Consider per-topic TTLs later. |
| SCOV-005 | Per-theater case discovery | Theater watch summary is now accepted and displayed, but live prompt compliance must be monitored. | Partial | `core/external_scout_packets.py`; `core/external_scout_threads.py`; `docs/AUTOSINT_THEATER_WATCH_POLICY.md` | Workstream `theater_watch_summary`. |
| SCOV-006 | Source-family coverage | Required packet matrices cover official/advisory, news, social, traffic, geospatial, weather, market, prediction, multilingual, and public comments. | Implemented | `core/external_scout_packets.py`; `config/autosint_sensor_coverage_policy.yml` | Monitor validation warnings for schema drift. |
| SCOV-007 | Claim/counter-claim/observed/advisory separation | Relationship buckets are required and shown operator-first. | Implemented | `core/external_scout_packets.py`; `core/api.py` | Keep raw relationship dumps in Audit Details. |
| SCOV-008 | Market/finance | Market subcategories are required and cue-only. | Implemented | `core/external_scout_packets.py`; `docs/AUTOSINT_GLOBAL_SENSOR_COVERAGE_POLICY.md` | Add insurance/freight detail if prompt output can support it. |
| SCOV-009 | Prediction markets | Polymarket and Kalshi rows are required; cue-only policy is enforced. | Implemented | `core/external_scout_packets.py`; `tests/test_external_scout_packets.py` | Add Manifold/other public market lane later if needed. |
| SCOV-010 | Social/public comments | Social OSINT and public comments are explicit, cue-only lanes. | Implemented | `core/external_scout_packets.py`; `config/autosint_sensor_coverage_policy.yml` | Preserve cue-only language in prompt artifacts. |
| SCOV-011 | Traffic/logistics | Traffic/movement appears in source family, case matrix, and thread source gaps. | Implemented | `core/external_scout_threads.py` | Add theater-specific traffic source hints in prompts. |
| SCOV-012 | Satellite/geospatial/weather | Geospatial and weather/environment are explicit lanes with context-only caveats where appropriate. | Implemented | `core/external_scout_packets.py`; `config/autosint_sensor_coverage_policy.yml` | Keep exact coordinates out of operator path. |
| SCOV-013 | Multilingual/regional | Multilingual context is required and validation catches missing status rows. | Implemented | `core/external_scout_packets.py`; `docs/AUTOSINT_THEATER_WATCH_POLICY.md` | Keep theater language lists current. |
| SCOV-014 | Quality warnings | Current and historical warnings are separated from current readiness. | Implemented | `core/external_scout_threads.py`; `core/api.py` | Keep historical warning details audit-only. |
| SCOV-015 | Validation/quarantine | Invalid packets fail closed and do not update current threads. | Implemented | `core/external_scout_packets.py`; capture package tests | Continue receipt-based proof. |
| SCOV-016 | UI/operator cards | Live Board shows current BLUF, deltas, source gaps, readiness, coverage, source checks, theater watch, and overflow. | Implemented | `core/api.py`; `tests/test_api_schema.py` | Operator readthrough after next natural cycle. |
| SCOV-017 | HAVOC/RFI consumption | HAVOC/RFI selects thread current state before raw packet fallback. | Implemented | `core/havoc_rfi_export.py`; `tests/test_havoc_rfi_export.py` | Keep preview separate from commander-ready. |
| SCOV-018 | PIR/priority questions | PIR Hunter exists but is not integrated as a thread overlay. | Future workstream | `config/autosint_workstreams.yml` | Workstream `pir_hunter_thread_overlay`. |
| SCOV-019 | Agent/scheduler integration | Launchd capture/prompt loop exists; agent scheduler is not primary. | Partial | `docs/status/AUTOSINT_WORKSTREAMS.md` | Keep future orchestration read-only first. |
| SCOV-020 | Retention/history | Current/stale/archive behavior is implemented. | Implemented | `core/external_scout_threads.py` | Continue natural-cycle retention tests. |
| SCOV-021 | Audit/provenance | Raw packet IDs, URLs, lineage, validation, and legacy linkage remain in Audit Details/provenance. | Implemented | `core/api.py`; `core/havoc_rfi_export.py` | Keep page dumps in review artifacts only. |
| SCOV-022 | Safety/no-write boundaries | Browser/API/report surfaces are read-only with mutation flags false. | Implemented | `AGENTS.md`; `core/api.py`; release surface tests | Do not add write controls without explicit approval. |
| SCOV-023 | 24/7 operations | Prompt-trigger/harvester/capture receipts and Live Board freshness are tracked. | Implemented | `config/autosint_workstreams.yml`; capture receipts | Continue :30 submit -> async harvest -> :00 capture monitoring. |
| SCOV-024 | Buyer/demo readiness | Multi-case board is live; global theater accountability is now visible but needs natural-cycle proof. | Needs test | `/external-scout/threads`; `docs/AUTOSINT_THEATER_WATCH_POLICY.md` | Verify next prompt/capture output includes theater summary and overflow if applicable. |

## Status Summary

- Implemented: thread identity, append/update, freshness, required matrices, relationship separation, cue-only policy, validation/quarantine, Live Board, HAVOC/RFI preview, retention/history, audit/provenance, safety.
- Partial: per-theater discovery, scheduler/agent integration.
- Needs test: live prompt compliance with `theater_watch_summary` and `overflow_candidate_cases`.
- Future workstream: PIR overlay, richer source quality scoring, optional orchestration observability.
