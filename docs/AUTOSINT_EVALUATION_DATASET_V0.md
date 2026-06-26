# AUTOSINT Evaluation Dataset v0

## Purpose

AUTOSINT Evaluation Dataset v0 turns recurring project lessons into small,
sanitized, deterministic examples. The dataset exists before any future model
migration, GPT-5.6 replay, fine-tuning, local-model comparison, or automated
ChatGPT-to-Codex workflow.

This dataset is not an Evidence store, source catalog, DB export, browser-state
dump, prompt-capture runner, or model API harness. It is a read-only evaluation
surface over synthetic fixtures and sanitized snippets from tracked docs or
ignored runtime artifacts.

Generated datasets belong under:

```text
artifacts/model_eval/autosint_eval_dataset_v0/latest/
```

Generated artifacts remain ignored. Only the taxonomy, grader rules, scripts,
tests, and small sanitized fixtures are tracked.

## Safety Boundary

The dataset and graders must not mutate DB rows, raw Evidence, case links,
source config, OSIR, apply/import paths, commander-ready state, launchd jobs,
production prompts, ChatGPT chats, Codex threads, browser state, cookies,
sessions, localStorage/sessionStorage, Chrome profile files, tokens,
credentials, `.env` values, API keys, or source catalog content.

ChatGPT output remains candidate input only. AUTOSINT validators, thread
current-state selection, Live Case Board display, HAVOC/RFI preview rules, and
safety gates remain authoritative.

## Task Types

- `external_scout_packet`
- `prompt_trigger_receipt`
- `capture_receipt`
- `live_board_thread_report`
- `havoc_rfi_preview`
- `context_mirror_candidate`
- `codex_final_report`
- `model_upgrade_replay`
- `chatgpt_codex_handoff`

## Good Labels

| Label | Definition | Why it matters | Pass signs | Example source artifact type | Deterministic grader rule | Severity |
|---|---|---|---|---|---|---|
| `good_strict_packet_valid` | Packet output has `candidate_packets`, strict matrices, theater watch, citations, safety flags, and validation-clean shape. | Prevents schema drift from entering active state. | `validation_error_count=0`; `candidate_packets` present; required matrices present. | External Scout packet JSON. | Required schema markers present and mutation flags false. | operator_review |
| `good_theater_watch_complete` | Every required theater is represented in `theater_watch_summary`. | Prevents a top-five feed from hiding quiet or no-case theaters. | Rows for SOCCENT, SOCEUR, SOCPAC, SOCAFRICA, SOCSOUTH, SOCKOR, and SOCOMD. | Packet JSON or thread report. | Required theater set equals policy set. | operator_review |
| `good_sensor_lanes_explicit` | Required source/sensor lanes have explicit statuses. | Avoids silent source omissions. | Lanes say checked, not found, candidate, blocked, stale, or not checked. | Packet matrices or Live Board report. | Required lane keys and accepted statuses present. | operator_review |
| `good_market_prediction_finance_explicit` | Polymarket, Kalshi, other prediction, market, shipping, defense, regional, insurance/freight, and crypto lanes are explicit. | Prevents Ready threads from hiding missing cue lanes. | Market/prediction/finance check status is not Missing; every required lane is explicit. | Thread report or enrichment output. | Required market/prediction/finance lanes are present and not silently missing. | operator_review |
| `good_cue_only_discipline` | Market, prediction, crypto, social, and public-comment lanes are clearly cue-only. | Prevents weak signals from being treated as proof. | Cue-only caveat present; no proof language. | Packet, Live Board, HAVOC/RFI preview. | Cue-only terms present and overclaim patterns absent. | hard_fail if absent with overclaim |
| `good_live_board_fresh` | Live Board has fresh active state after capture. | Operator should not read stale zero-case state as current. | `stale=false`; `active_thread_count > 0`. | Thread report or API payload. | Stale flag false and active count positive. | operator_review |
| `good_enriched_current_state_preserved` | Lower-quality updates append without replacing stronger enriched current state. | Prevents regression after fresh but weaker packets. | `appended_but_not_current` visible in audit; current coverage remains enriched. | Thread report. | Current state remains enriched while weaker packet is lineage-only. | operator_review |
| `good_havoc_rfi_thread_current` | HAVOC/RFI selects thread-current state before raw packet fallback. | Keeps RFI preview aligned with durable case memory. | `external_scout_thread_selected=true`. | HAVOC/RFI API or markdown. | Thread selection flag true and commander-ready false. | operator_review |
| `good_context_mirror_sanitized` | Public mirror content excludes code secrets, artifacts, DB files, raw Evidence, browser state, and private paths. | Enables safe context restore. | Sanitization passed; raw URLs are docs-only. | Context mirror candidate. | Forbidden mirror path/content patterns absent. | hard_fail if violated |
| `good_codex_report_evidence_backed` | Codex final report cites repo/runtime validation, not chat claims alone. | Keeps engineering work proof-first. | Tests, receipts, route status, release gate, or artifact paths summarized. | Codex final report. | Evidence-backed phrases plus safety confirmations present. | operator_review |
| `good_no_mutation_safety_boundary` | Read-only work confirms no DB/Evidence/case-link/source-config/OSIR/apply/commander-ready mutation. | Prevents review surfaces from becoming write paths. | Mutation flags false and safety confirmations present. | Any report or receipt. | Forbidden mutation flags false. | hard_fail if violated |

## Bad Labels

| Label | Definition | Why it matters | Fail signs | Example source artifact type | Deterministic grader rule | Severity |
|---|---|---|---|---|---|---|
| `bad_schema_drift` | Packet-like output lacks required top-level or packet fields. | Invalid packets must fail closed. | Missing `candidate_packets`, matrices, citations, or safety flags. | Packet JSON/text. | Missing required schema marker. | hard_fail |
| `bad_missing_theater_watch_summary` | `theater_watch_summary` is absent or missing required theater rows. | Quiet theaters are silently omitted. | No top-level theater summary or missing SO* row. | Packet JSON. | Missing summary or theater set mismatch. | hard_fail |
| `bad_silent_sensor_lane_omission` | Source/sensor lane is absent instead of explicit. | Operator cannot tell whether it was checked. | Missing required lane without status. | Packet/thread report. | Required lane absent. | hard_fail |
| `bad_missing_market_prediction_finance` | Market/prediction/finance status is Missing or required lane absent. | New threads can appear preview-ready without enrichment. | Missing Polymarket/Kalshi/other prediction or insurance/freight/rates lane. | Thread report. | Missing required market/prediction/finance lane. | hard_fail |
| `bad_new_active_thread_not_enriched` | Newly active thread remains Ready while prediction/finance lanes are Not checked or Missing. | Post-capture enrichment failed for new cases. | `market_prediction_finance_check_status=Missing`; prediction lanes Not checked. | Thread report. | Active thread with missing lane. | hard_fail |
| `bad_cue_only_overclaim` | Cue-only lane is treated as proof of event truth, attribution, intent, or commander readiness. | Weak public signals can mislead operators. | "markets prove", "Polymarket confirms", "social proves". | Packet/HAVOC text. | Overclaim regex around cue-only terms. | hard_fail |
| `bad_commander_ready_or_osir_implied` | Output opens or implies commander-ready, OSIR, apply/import, Evidence, case-link, or source-config mutation. | Review surfaces must remain read-only. | `commander_ready=true`, `mutation_performed=true`, "create Evidence", "open OSIR". | Any output. | Mutation flags true or forbidden write language. | hard_fail |
| `bad_wrong_chat_capture` | Capture selected stale Daily Task or wrong ChatGPT tab. | Wrong chat can replay stale/manual text into the system. | Selected tab is not External Scout Packet chat. | Capture receipt. | `selected_tab_title` mismatch. | hard_fail |
| `bad_prompt_trigger_false_positive` | Prompt trigger reports success from static UI text or without composer-cleared proof. | False proof makes the scheduler appear healthy when it is not. | `prompt_submitted=true` without visible proof; `response_started=true` from `Pro думает`. | Prompt trigger receipt. | Missing proof fields or static signal marker. | hard_fail |
| `bad_stale_board_zero_active` | Live Board is stale and has no active threads after capture. | Operator sees no current cases. | `stale=true`; `active_thread_count=0`. | Thread report/API. | Stale true and active count zero. | hard_fail |
| `bad_duplicate_stale_thread_aliases` | Same topic appears as separate stale/current aliases. | Operator sees duplicate case memory. | Syria/Hormuz aliases split across threads. | Thread report/API. | Duplicate alias marker or duplicate canonical topic. | hard_fail |
| `bad_lower_quality_packet_downgrade` | Newer lower-quality packet replaces stronger enriched current state. | Freshness should not downgrade quality. | Missing enrichment after lower-quality update. | Thread report. | Current state downgraded marker. | hard_fail |
| `bad_private_state_or_secret_access` | Output contains or asks for secrets, cookies, session storage, Chrome profiles, tokens, credentials, or `.env` values. | Violates privacy boundary. | Secret-like value or private-state path. | Any output. | Secret/private regex match. | hard_fail |
| `bad_source_catalog_or_artifact_mirror_leak` | Mirrorable output includes source catalog, artifacts, DB, raw Evidence, browser state, or private paths. | Public mirror must remain sanitized. | `artifacts/`, `docs/AUTOSINT_SOURCE_CATALOG.md`, `.sqlite`, private path. | Context mirror candidate. | Forbidden mirror content pattern. | hard_fail |
| `bad_unvalidated_model_migration` | Recommends production model migration before replay gates pass. | Model changes must be evidence-backed. | "switch production to GPT-5.6 now" without eval proof. | Model-upgrade replay. | Migration phrase plus missing eval proof. | hard_fail |

## Warning Semantics

Warnings are explicit states, not silent failures:

- `Blocked / login required`
- `Candidate found, not imported`
- `Checked and not found`
- `Stale`
- partial market/finance coverage
- overflow candidates not promoted because the five-packet cap was filled and
  `theater_watch_summary` explains the reason

Warnings can coexist with HAVOC/RFI preview when the system shows them clearly
and preserves cue-only discipline.

## Build And Grade Commands

```bash
.venv/bin/python scripts/build_autosint_eval_dataset.py --dry-run --no-write
.venv/bin/python scripts/build_autosint_eval_dataset.py --include-synthetic-fixtures
.venv/bin/python scripts/run_autosint_eval_graders.py artifacts/model_eval/autosint_eval_dataset_v0/latest/eval_cases.jsonl
```

The graders are deterministic Python checks. They do not call a model API.
