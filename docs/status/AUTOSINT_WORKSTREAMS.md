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
| `global_sensor_coverage_policy` | Active | Enforce no-silent-omission source/sensor coverage policy across packets, reports, Live Board, and HAVOC/RFI preview. |
| `theater_watch_summary` | Complete | Live Packet output now reports checked/no-case/overflow state for SOCCENT, SOCEUR, SOCPAC, SOCAFRICA, SOCSOUTH, SOCKOR, and SOCOMD. |
| `chatgpt_project_operating_model` | Complete | Keep ChatGPT Project chats as workspaces, not case memory. |
| `context_mirror_automation` | Active | Keep public sanitized context mirror current after source-of-truth changes. |
| `external_scout_capture_isolation` | Complete | Keep capture code isolated behind the package CLI and launchd wrapper. |
| `pir_hunter_thread_overlay` | Planned | Design PIR Hunter as a priority-question overlay on Live Case Board threads. |
| `havoc_rfi_thread_current` | Active | Keep HAVOC/RFI consuming thread current state before packet fallback. |
| `source_catalog_policy` | Blocked | Await explicit decision before tracking or mirroring source catalog policy. |
| `launchd_runtime_health` | Complete | Scheduled capture fired naturally at `:08` with clear receipts and fresh Live Case Board state. |
| `external_scout_multi_case_board` | Complete | Multi-case prompt, partial-promotion guard, rolling current/stale/archive retention, and natural-cycle proof are complete. |
| `chatgpt_scheduled_tasks_production_path` | Needs Verification | Move External Scout upstream generation back to ChatGPT Scheduled Tasks as primary only after two natural capturable output cycles; local prompt trigger remains production upstream until then. |
| `orchestration_prefect_spike` | Planned | Evaluate Prefect as a read-only observability wrapper over the current local loop. |
| `agent_pir_langgraph_design` | Planned | Design future read-only LangGraph agent loops for PIR/source-gap/thread review. |
| `local_knowledge_index_spike` | Planned | Design a sanitized local retrieval index over docs, context mirror, page dumps, briefs, and receipts. |
| `run_observability_dashboard` | Planned | Design a local read-only run dashboard over receipts, status JSON, workstreams, and context mirror health. |
| `gpt56_model_upgrade_evaluation` | Needs Verification | Evaluate GPT-5.6 model-family availability and non-production AUTOSINT replay before any production migration. |
| `autosint_eval_dataset_v0` | Active | Maintain sanitized AUTOSINT eval taxonomy, deterministic graders, safe fixtures, and copy-safe ChatGPT-to-Codex handoff queue. |

## Next Recommended Codex Task

Theater-watch summary is verified. The 2026-06-25 short-loop Packet-chat
prompt/capture proof promoted receipt `20260625T165421Z_capture_receipt.json`
with `validation_error_count=0`, generated_at `2026-06-25T16:50:51Z`, five
valid packets, seven normalized `theater_watch_summary` rows, and three
`overflow_candidate_cases`.

The next natural `:08` capture also proved the production path. Receipt
`20260625T170810Z_capture_receipt.json` promoted generated_at
`2026-06-25T16:51:19Z` with `validation_error_count=0`, five valid packets,
seven normalized theater rows, three overflow candidates, and Live Case Board
`stale=false`.

Normalized theater rows accounted for every required theater:
`SOCCENT`, `SOCEUR`, `SOCPAC`, `SOCAFRICA`, `SOCSOUTH`, `SOCKOR`, and
`SOCOMD`. Status counts were `active_case_found=3`, `no_active_case=1`, and
`omitted_or_overflow=3`. Continue routine hourly monitoring; reopen the
workstream only if a future capture omits a required theater row or fails to
surface no-case/overflow state.

Current prompt-trigger note: short-interval wrapper tests after the verifier
hardening promoted strict Packet-chat captures at `2026-06-25T00:16:46Z` and
`2026-06-25T00:25:45Z`. The first natural post-patch cycle also passed:
`20260625T005007Z` prompt receipt showed Packet-chat delivery and
`20260625T010810Z` capture promoted generated_at `2026-06-25T00:40:00Z`
with `validation_error_count=0` and Live Case Board `stale=false`.

Follow-up short-loop debugging found one more verifier false positive:
static ChatGPT UI copy containing `Pro думает` was being counted as a
busy/response-started signal. Commit `5e78beb` removed that false signal from
prompt-trigger verification. After the fix, trigger receipt
`20260625T011928Z` submitted to the Packet chat; Intelligence Pro generation
took several minutes; dry-run found a new strict packet generated_at
`2026-06-25T01:20:19Z` with `validation_error_count=0`; and capture receipt
`20260625T012932Z` promoted it with Live Case Board `stale=false`. Development
debugging should use this short trigger -> dry-run -> capture loop instead of
waiting for the next hourly window.

Multi-case proof passed after the multi-case implementation:
trigger receipt `20260625T021124Z` submitted the Packet-chat prompt and
detected an assistant response; dry-run found four valid packets generated_at
`2026-06-25T01:28:50Z` with `validation_error_count=0`; capture receipt
`20260625T022732Z` promoted all four; and Live Case Board reported four active
threads, all `Ready for HAVOC/RFI Preview`, with `stale=false`.

The first post-proof `23:10` check was mixed but operational: prompt receipt
`20260625T025006Z` failed with
`prompt_submit_failed:submit_not_verified_composer_not_cleared`, but capture
receipt `20260625T030809Z` still selected the Packet chat and promoted four
valid packets generated_at `2026-06-25T01:45:00Z` with
`validation_error_count=0`. Subsequent natural cycles from
`20260625T035009Z/040807Z` through `20260625T125007Z/130810Z` submitted
prompts, detected assistant responses, and promoted four to five valid packets
with `validation_error_count=0`. Latest verified Live Case Board state is
`stale=false` with five active threads.

Launchd runtime repair note: on 2026-06-27, both External Scout LaunchAgents
were failing pre-exec with `EX_CONFIG` before wrapper logs were written. The
installed plists were repaired by removing unused `StandardOutPath` and
`StandardErrorPath` entries; the wrapper scripts already write timestamped
ignored logs under `artifacts/external_scout/*_logs/`. After reloading only
`com.autosint.external-scout-prompt-trigger` and
`com.autosint.external-scout-capture`, launchd kickstart proof produced prompt
receipt `20260627T015843Z` with `packet_ready_for_capture=true`,
`strict_packet_validation_error_count=0`, and generated_at
`2026-06-27T02:00:00Z`. Capture receipt `20260627T021023Z` then promoted five
valid packets with `validation_error_count=0`; Live Case Board reported
`stale=false`, five active threads, one stale tracked thread, and eval v1
reported no current runtime hard-fails. Verify the next natural `:50 -> :08`
cycle to close the production-schedule proof after this local LaunchAgent
repair.

Evaluate `orchestration_prefect_spike` only as a read-only observability
wrapper. Do not replace launchd or add agent/write automation in that spike.

New model-family evaluation is now tracked as
`gpt56_model_upgrade_evaluation`. It is not a production migration approval.
Next proof should verify actual ChatGPT/Codex/API availability without reading
secrets or private browser state, then run sanitized offline replay against the
strict External Scout packet contract, Live Case Board readability, and
HAVOC/RFI review-only boundaries.

`autosint_eval_dataset_v0` now supports the model-upgrade workstream with a
sanitized label taxonomy, deterministic local graders, committed safe fixtures,
ignored generated datasets, and a copy-safe ChatGPT review to Codex handoff
queue. It does not scrape ChatGPT, read browser state, call model APIs, mutate
runtime state, or approve production model migration by itself.

`chatgpt_scheduled_tasks_production_path` is tracked as Needs Verification. The target
operating model is ChatGPT Scheduled Tasks as the primary upstream generator
for strict External Scout packets; AUTOSINT capture, validator, quarantine,
Live Case Board, health monitor, and eval remain the source of truth. The
local Packet-chat prompt trigger remains the current proven production upstream
until an existing Scheduled Task can be safely configured and two natural
Scheduled Task -> capture cycles are proven. On 2026-06-28, a fallback
prompt-trigger foreground drift inserted
a draft into the non-target `autosint` chat; the draft was cleared, target
scripts were hardened to revalidate the foreground Packet tab before executing
JavaScript, and recovery receipts `20260628T174230Z_prompt_trigger_receipt.json`
and `20260628T175854Z_capture_receipt.json` proved Packet-chat delivery,
request-id match, `validation_error_count=0`, four promoted packets, and Live
Board `stale=false`. Later on 2026-06-28 the live
Scheduled Tasks UI showed `AUTOSINT Daily External Scout` was paused and still
had a stale prompt. The existing task was updated from the current strict local
prompt artifact and resumed. The first proof window did not produce a usable
capture target: the task stayed visible as `Выполняется` for more than ten
minutes, exposed no run-now or result-chat link, did not create a new open
task-output tab, and did not advance the Packet chat before the natural `:08`
capture. Capture receipt `20260628T190806Z_capture_receipt.json` correctly
selected the Packet chat and safe-skipped `older_than_latest_inbox`. The local
fallback LaunchAgent was restored; prompt receipt
`20260628T192327Z_prompt_trigger_receipt.json` and capture receipt
`20260628T193810Z_capture_receipt.json` recovered Live Board `stale=false`
with five active packets generated_at `2026-06-28T19:24:32Z`. An outside-project
task-result conversation later appeared with generated_at `2026-06-28T19:34:28Z`, but
dry-run validation against the exact conversation failed with twelve
`source_relationships` bucket type errors. The live Scheduled Task prompt and
ignored prompt artifact were tightened to require array buckets, but the next
Scheduled Task run again stayed visible as `Выполняется` while the local Packet
fallback generated `2026-06-28T20:06:30Z`; capture receipt
`20260628T200809Z_capture_receipt.json` promoted five valid packets. Scheduled
Task proof now uses the dedicated scheduled-task capture probe so invalid or
late task output cannot disturb the working Packet target. The first probe
receipt `20260628T202500Z_scheduled_task_capture_probe_receipt.json` selected
the task-result conversation and found `packet_count=5`,
`validation_error_count=0`, and generated_at `2026-06-28T20:05:53Z`, but
safe-skipped because the Packet fallback inbox was already newer. That
outside-project result chat was deleted by the user and must not be used as a
production target. The Scheduled Tasks page currently shows
`AUTOSINT Daily External Scout` paused; keep it paused unless a Project-scoped
output path is available.

## Safety Boundary

Workstream tracking is memory and verification only. It does not mutate DB,
Evidence, case links, source config, OSIR, apply/import paths, launchd, or
commander-ready state.
