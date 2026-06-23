# AUTOSINT Workstreams

This tracked status file defines the current long-running AUTOSINT workstreams.
The structured source of truth is `config/autosint_workstreams.yml`; generated
reports belong under ignored `artifacts/autosint_workstreams/latest/`.

## Current Operating Loop

```text
finding -> validation -> dedupe -> false-positive check -> targeted fix -> tests -> release surface -> context mirror -> human boundary
```

## Seeded Workstreams

| Workstream | Current status | Purpose |
| --- | --- | --- |
| `external_scout_strict_capture` | Complete | Natural hourly strict ChatGPT output validated and promoted through staging overnight. |
| `external_scout_live_case_board` | Active | Keep `/external-scout/threads` current, fresh, and operator-readable. |
| `case_coverage_matrix` | Active | Maintain full strict coverage matrices in packets and thread rollups. |
| `chatgpt_project_operating_model` | Complete | Keep ChatGPT Project chats as workspaces, not case memory. |
| `context_mirror_automation` | Active | Keep public sanitized context mirror current after source-of-truth changes. |
| `external_scout_capture_isolation` | Complete | Keep capture code isolated behind the package CLI and launchd wrapper. |
| `pir_hunter_thread_overlay` | Planned | Design PIR Hunter as a priority-question overlay on Live Case Board threads. |
| `havoc_rfi_thread_current` | Active | Keep HAVOC/RFI consuming thread current state before packet fallback. |
| `source_catalog_policy` | Blocked | Await explicit decision before tracking or mirroring source catalog policy. |
| `launchd_runtime_health` | Complete | Scheduled capture fired naturally at `:08` with clear receipts and fresh Live Case Board state. |

## Next Recommended Codex Task

Keep monitoring `source_catalog_policy` for the explicit tracking decision, and
reopen capture workstreams only if scheduled receipts stop, quarantine strict
output, or Live Case Board freshness diverges from the latest valid capture.

## Safety Boundary

Workstream tracking is memory and verification only. It does not mutate DB,
Evidence, case links, source config, OSIR, apply/import paths, launchd, or
commander-ready state.
