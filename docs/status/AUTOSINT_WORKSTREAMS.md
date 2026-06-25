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
| `external_scout_multi_case_board` | Needs Verification | Fix the current one-case board gap by producing multiple strict current packets and/or retaining stale active threads. |
| `orchestration_prefect_spike` | Planned | Evaluate Prefect as a read-only observability wrapper over the current local loop. |
| `agent_pir_langgraph_design` | Planned | Design future read-only LangGraph agent loops for PIR/source-gap/thread review. |
| `local_knowledge_index_spike` | Planned | Design a sanitized local retrieval index over docs, context mirror, page dumps, briefs, and receipts. |
| `run_observability_dashboard` | Planned | Design a local read-only run dashboard over receipts, status JSON, workstreams, and context mirror health. |

## Next Recommended Codex Task

Work `external_scout_multi_case_board` next. Current production prompt-trigger
output is intentionally one highest-priority packet, while older multi-topic
history predates the strict matrix contract and is skipped from current thread
state. The product fix should be scoped separately: produce up to five strict
current packets per cycle and add a rolling active/stale thread retention model.

Current prompt-trigger note: short-interval wrapper tests after the verifier
hardening promoted strict Packet-chat captures at `2026-06-25T00:16:46Z` and
`2026-06-25T00:25:45Z`. Natural `:50 -> :08` proof is still required before
the current 24/7 loop is considered re-verified after this patch.

After that, evaluate `orchestration_prefect_spike` as a read-only observability
wrapper. Do not replace launchd or add agent/write automation in that spike.

## Safety Boundary

Workstream tracking is memory and verification only. It does not mutate DB,
Evidence, case links, source config, OSIR, apply/import paths, launchd, or
commander-ready state.
