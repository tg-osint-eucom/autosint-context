<!-- GENERATED FILE: scripts/render_autosint_workstreams_current.py --write -->
# AUTOSINT Workstreams

- Status: Current projection
- Authority: Supporting status; `config/autosint_workstreams.yml` is the structured source
- Owner: AUTOSINT Workstreams
- Last reviewed: 2026-07-18
- Runtime truth: No; current runtime requires receipts and canonical reports
- Supersedes: Mixed current projection and embedded runtime-history narrative
- Superseded by: None
- Source config SHA-256: `aa7631ad02edeb5e919ef10f4b53aa32a3879b4e0f93edb80ce8d3201c4ad0ce`

This generated projection exposes only durable planning identity and status.
Detailed registry notes are planning context, not current runtime proof. Dated
prompt, harvest, health, packet, and proof claims belong in receipts or ignored
generated reports and are never merged into this table.

| Workstream | Title | Status | Owner / surface |
|---|---|---|---|
| `external_scout_strict_capture` | External Scout manual direct capture diagnostics | `Complete` | External Scout manual capture bridge / ChatGPT Project |
| `external_scout_live_case_board` | External Scout Live Case Board | `Active` | /external-scout/24-7 with /external-scout/threads drill-down |
| `case_coverage_matrix` | Strict case coverage matrix | `Active` | External Scout validator / thread rollups |
| `global_sensor_coverage_policy` | Global source and sensor coverage policy | `Active` | External Scout validator / Live Case Board / prompt contract |
| `theater_watch_summary` | Global seven-theater sweep, cross-theater dedup, and rotating deep dives | `Active` | External Scout prompt/normalizer/validator / same-source /external-scout/24-7 panel |
| `chatgpt_project_operating_model` | ChatGPT Project operating model | `Complete` | ChatGPT Project / docs |
| `context_mirror_automation` | Public context mirror automation | `Active` | scripts/publish_autosint_context_mirror.py |
| `external_scout_capture_isolation` | External Scout capture subsystem isolation | `Complete` | autosint_external_scout_capture package |
| `pir_hunter_thread_overlay` | PIR Hunter thread overlay | `Planned` | PIR Hunter / Live Case Board future integration |
| `rfi_thread_current` | RFI thread-current consumption | `Active` | RFI package preview |
| `source_catalog_policy` | Source catalog policy | `Blocked` | source catalog / source policy |
| `launchd_runtime_health` | Launchd runtime health | `Complete` | com.autosint.external-scout-prompt-trigger / com.autosint.external-scout-findings-harvester |
| `external_scout_24_7_proof_loop` | External Scout 24/7 proof loop | `Active` | /external-scout/24-7 canonical proof report over prompt, harvest, promotion receipts / health monitor / eval |
| `external_scout_async_findings_harvester` | External Scout async Scout Findings harvester | `Active` | Packet v2 Scout Findings prompt-trigger / harvester receipts / normalized capture path |
| `external_scout_multi_case_board` | External Scout multi-case Live Board | `Complete` | External Scout prompt trigger / Live Case Board |
| `chatgpt_scheduled_tasks_production_path` | ChatGPT Scheduled Tasks production path | `Blocked` | ChatGPT Scheduled Tasks / Scheduled Task output chat / Packet fallback / capture bridge |
| `orchestration_prefect_spike` | Prefect orchestration observability spike | `Planned` | Future local ops orchestration |
| `agent_pir_langgraph_design` | LangGraph PIR and reviewer agent design | `Planned` | Future PIR/source-gap/thread-review agents |
| `local_knowledge_index_spike` | Local AUTOSINT knowledge index spike | `Planned` | Future LlamaIndex/local retrieval layer |
| `run_observability_dashboard` | External Scout 24/7 pinned operator source | `Active` | /external-scout/24-7 canonical proof page |
| `sensor_architecture_v1` | AUTOSINT sensor architecture v1 | `Active` | /external-scout/24-7 canonical proof page |
| `gpt56_model_upgrade_evaluation` | GPT-5.6 Sol Pro production-selection verification | `Needs Verification` | ChatGPT Pro / Extended selection / offline replay / AUTOSINT validation gates |
| `autosint_eval_dataset_v0` | AUTOSINT evaluation dataset v0 | `Active` | Evaluation dataset / deterministic graders / ChatGPT-Codex handoff queue |

## Runtime Boundary

A `Complete` or `Active` workstream status is planning state, not proof that a
current External Scout cycle, route, service, or data source is healthy. Use
the canonical proof, health, thread, and route reports for live claims.
