# AUTOSINT Repository Constitution

This file is the concise, durable constitution for Codex work in AUTOSINT.
Tracked policy and current receipt-backed evidence remain authoritative for the
specific fields they own; this constitution defines the boundaries between
them.

## 1. Authority and repository boundary

- **Evidence hierarchy.** Obey product/system safety and the explicit task,
  then the nearest applicable `AGENTS.override.md` or `AGENTS.md`, current
  tracked code/docs/config/schema/tests, current timestamped receipt-backed
  runtime evidence, the sanitized public mirror, Codex memory, the current
  thread, and only then older reports or screenshots. More local, current, and
  field-specific authority wins. Report conflicts and timestamps; never merge
  fields from different snapshots into one claimed-current state.
- **Proof first.** Inspect repository and runtime evidence before making
  current-state claims. Model confidence, prior chat, plans, screenshots,
  announcements, old reports, and HTTP availability are never substitutes for
  the applicable validator, receipt, route data contract, or release gate.
- **Canonical boundary.** Current work belongs only in
  `autosint-clean-20260621`. `autosint-context` is the sanitized public context
  mirror. `autosintmvp` is legacy/archive and may be used only for an explicitly
  historical task. Never perform current work in the stale `autOSINT` checkout.
  Do not create another permanent checkout, worktree, fork, or truth source
  without an explicit architecture task.
- **Repository preflight.** Before any AUTOSINT action, run `pwd`, verify the
  absolute repository root, branch, and HEAD, inspect
  `git status --short --untracked-files=all`, and inspect staged and unstaged
  diffs. Preserve unrelated user changes and stop on a wrong boundary.
- **Current authority bundle.** Before substantial architecture, runtime,
  External Scout, UI, Mission Control, Threads, RFI, sensor, model,
  integration, or mirror work, read the relevant tracked sources listed in
  section 11, including `AGENTS.md`, the current operating model, primary
  workflow, External Scout runbook, and workstream status. Read the relevant
  core/config/routes/tests before a sensitive subsystem change; module, model,
  config-row, MCP-tool, route, or helper existence alone does not prove
  integration.
- **OpenAI product truth.** For OpenAI, ChatGPT, Codex, model, SDK, MCP,
  permission, pricing, or rollout behavior, use current official OpenAI
  documentation. Distinguish documented support from availability in this
  installation/account; do not inspect private account state or make a
  credentialed call unless the task explicitly authorizes it.
- **Memory boundary.** Codex memory is helper recall only and cannot override
  repository/runtime evidence. Durable rules live in tracked sources; the
  current thread is temporary. Use `/goal` for substantial multi-phase work.
  When supported, helper recall may be enabled with `[features] memories = true`.

## 2. Product invariants

- **Approved scope phrase.** Describe this program as a
  `production-grade foundation for a controlled SOCOM pilot`. Do not claim an
  official OpenAI partnership, SOCOM production authorization, ATO,
  classified-network approval, commander-ready authority, exhaustive global
  coverage, or full production readiness before the acceptance matrix passes.
- **One operator application.** Preserve one AUTOSINT server/app shell, one
  External Scout proof source, one Live Board, and one case-memory system. The
  target primary navigation is `MISSION`, `WATCH`, `CASES`, `PIR`, `AGENTS`,
  `RFI`, and `SYSTEM`; deep legacy-compatible routes may remain bounded
  audit/drill-down views during migration. Never add a competing app server,
  dashboard, control plane, proof builder, board, or case store.
- **Primary operator truth.** `/external-scout/24-7` and its same-source proof
  object/API remain the pinned External Scout truth surface. `/mission-control`,
  `/external-scout`, `/external-scout/threads`, `/rfi`, `/rfi/SOCCENT`, and
  canonical supporting JSON/audit routes are supporting read-only surfaces.
  `/dagrbook`, `/moltbook`, and `/control-plane` remain `LEGACY_REMOVED` unless
  a future tracked architecture decision explicitly supersedes that status.
- **Canonical workflow.** Preserve
  `Mission Control -> External Scout Live Case Board -> RFI -> future controlled approval`.
  Model/ChatGPT output is candidate input only. `/external-scout/threads` owns
  durable thread-current case memory; `/external-scout` is the active packet
  inbox/support view; RFI consumes thread-current state first and validated
  packet fallback only when thread-current state is unavailable.
- **PIR Hunter.** PIR Hunter is a current read-only mission-question and
  collection-gap capability. It derives status from validated case/thread/source
  evidence and explicit operator state; it cannot create Evidence, mutate
  cases or source configuration, open OSIR, apply/import, set commander-ready,
  or declare a PIR answered from model text alone.
- **Agent Collaboration Room.** `AGENTS` is a current inspectable capability
  for team, room, runs, tasks, handoffs, critiques, tools, guardrails, and
  audit. Human-readable feed items must map to typed stored events; the room is
  not an unbounded peer-chat network and is not mutation authority.
- **Production preservation.** Preserve the current External Scout production
  default until a separately approved migration gate changes it. PIR and Agent
  implementation must not redefine External Scout proof, thread-current state,
  Evidence, OSIR, case linkage, apply/import, or commander-ready status.

## 3. Architecture boundaries

- **External Scout chain.** Preserve
  `Scout Findings -> deterministic normalization -> structural validation -> semantic validation -> preservation validation -> quarantine or promotion -> durable Threads -> read-only RFI`.
  Direct `candidate_packets` is an explicit fallback/replay mode only, never a
  simultaneous production default. Invalid, mismatched, expired, stale, or
  schema-drifted capture fails closed.
- **Canonical builders.** Extend existing canonical builders and state sources;
  do not create a second app, proof reporter, dashboard, collector, normalizer,
  scheduler, case memory, or parallel truth. Read-only aggregation may consume
  canonical APIs but may not invent state.
- **External Scout control plane.** New 24/7 operator sections read from the
  canonical proof builder. Threads, RFI, JSON, logs, artifacts, and audit views
  remain drill-downs, not lifecycle controls. The ChatGPT Project is a
  workspace; AUTOSINT Threads are durable case memory.
- **Sensor contract.** Broad discovery is candidate planning input;
  deterministic adapters, normalizers, validators, promotion gates, Live Board,
  health, and RFI own the later stages. No required sensor lane may be silently
  omitted. Sensor changes must follow the tracked architecture, global
  coverage, theater-watch, market, runbook, config, and focused tests listed in
  section 11.
- **Theater and enrichment contract.** A cycle may emit at most five active
  packets, while `theater_watch_summary` accounts for `SOCCENT`, `SOCEUR`,
  `SOCPAC`, `SOCAFRICA`, `SOCSOUTH`, `SOCKOR`, and `SOCOMD`. Overflow has an
  explicit reason, source-family status, and next check and cannot replace
  active state without valid promotion. Market/prediction/finance enrichment
  explicitly represents Polymarket, Kalshi, other prediction markets, broad
  market, oil/energy, shipping/tanker, defense large-cap and mid/small,
  represented foreign/regional markets, insurance/freight/rates, and
  crypto/risk; all remain cue-only.
- **Model/evaluation boundary.** Model announcements and review text are input,
  not runtime truth. Production prompts, validators, routing, readiness, and
  schedules do not change until non-production replay proves intended-surface
  availability, strict coverage/cue-only validation, no prohibited mutation,
  latency, reliability, and cost. Models may assist; deterministic validators
  and canonical route/report output remain authoritative. Generated evaluation
  cases/packages stay sanitized and ignored.
- **Handoff and workstream boundary.** The ChatGPT-to-Codex handoff is
  sanitized file/copy-safe input only unless a future official path is verified
  and approved; no private URL scraping, browser state, AppleScript/System
  Events, clipboard, or auto-posting. Workstream tracking comes from
  `config/autosint_workstreams.yml`, its status doc, and the dry-run reporter;
  it is project memory, never a write/action path.

## 4. Agent/tool rules

- **Typed event store.** Every Agent Room item maps to one of the allowlisted
  event types (`agent_message`, task lifecycle, tool request/result, handoff,
  finding/challenge, critique, evidence gap, revision/rejection, run result, or
  human review/decision) and retains `event_id`, `run_id`, `task_id`,
  `parent_event_id`, `agent_role`, `recipient_role`, `event_type`, `created_at`,
  `structured_payload`, `source_references`, `limitations`,
  `guardrail_status`, and `mutation_performed=false`. No agent may silently
  communicate outside this store.
- **Bounded runtime modes.** `deterministic_replay` is enabled for tests/demo
  and `local_test` for a bounded local operator demo. `openai_staging` and
  `production` default disabled. An optional Agents SDK adapter may exist, but
  this program does not authorize an OpenAI API call, API-key read, or provider
  enablement; staging needs a separate approval and replay gate.
- **Manager orchestration.** The manager invokes bounded specialists as tools.
  A typed handoff is allowed only to an allowlisted destination, with validated
  input, minimum filtered context, preserved provenance, enforced maximum
  depth, and passing guardrails. Do not implement an uncontrolled agent social
  network.
- **Agent authority ceiling.** No agent or tool may upgrade candidate material
  to Evidence, promote a packet, mutate cases or sources, open OSIR,
  apply/import, set commander-ready, change proof history, reset rotation, or
  bypass deterministic validators. PIR and agent observations are advisory;
  human review remains required.
- **MCP default.** MCP starts from the canonical repository and is read-only by
  default. Writes require the global gate, exact mutation-class gate,
  `allow=true`, exact scope, deterministic policy checks, and an audit receipt;
  otherwise fail closed. Follow
  `docs/architecture/AUTOSINT_MCP_BOUNDARY_V1.md`; tool or transport
  availability alone does not confer mutation authority.
- **Runtime tool discipline.** Start read-only. Do not trigger manual External
  Scout prompts, harvesters, recovery, direct capture, browser/Chrome actions,
  launchd changes, duplicate lifecycle actions, collectors, Operator Scheduler,
  or `core.worker` integration unless the exact current task authorizes that
  action. A pending matching request must finish naturally or be reported
  honestly; do not manufacture proof.

## 5. Data/evidence/provenance

- **Candidate boundary.** Search results, Scout Findings, source URLs, model
  text, PIR observations, Agent events, HTTP 200, and discovery rows are not
  Evidence, verified coverage, case links, OSIR, apply/import, or
  commander-ready output. HTTP 200 proves availability only. Deterministic
  AUTOSINT validation and explicit promotion gates are authoritative.
- **Evidence integrity.** Never mutate raw Evidence to improve UI or tests.
  Temporal Guardian policy/code owns freshness and TTL; do not duplicate it in
  collectors or UI. OSIR remains policy-gated and cannot be bypassed from a
  review surface.
- **Contract identity.** Machine-owned `expected_contract_* -> bound_contract_* -> validation_contract_*`
  identity selects validation and promotion authority. Model-reported identity
  is diagnostic only. Preserve request/turn binding, source references,
  timestamps, limitations, validation results, and receipt provenance.
- **Truth axes and states.** Proof, theater coverage, rotation, runtime health,
  and release readiness are separate axes. Keep `current`, `retained`, `stale`,
  `blocked`, `candidate-only`, `not-checked`, `unavailable`, and `unknown`
  explicit; never relabel retained or stale data as current or combine
  incompatible snapshots.
- **Coverage vocabulary.** Every required source/sensor lane reports one of
  `Checked and found`, `Checked and not found`,
  `Candidate found, not imported`, `Not checked`, `Stale`, or
  `Blocked / login required`. A structural placeholder, candidate URL, source
  label, or plausible domain does not count as checked coverage.
- **Cue-only limits.** Market, crypto, prediction-market, social/public
  reaction, and public-comment lanes may provide context but cannot
  independently prove attribution, causality, intent, closure/reopening,
  insider activity, Evidence, OSIR, case linkage, apply/import, or
  commander-ready status.
- **Capture preservation.** Capture writes only ignored staging, inbox,
  quarantine, latest, receipt, and log artifacts. Generated artifacts remain
  under `artifacts/` and uncommitted. Lower-quality valid packets may append to
  history but may not replace best current state; stale/archive threads are
  visibly separate from current active threads.

## 6. Human approval/mutation

- **Closed by default.** Database, raw Evidence, case-link, source registry or
  configuration, OSIR, apply/import, commander-ready, production model/prompt,
  launchd, collector, Agent/PIR write, Operator Scheduler, and browser-lifecycle
  mutation are closed unless the current task explicitly authorizes the exact
  target and every tracked gate passes. A read-only review surface remains
  read-only.
- **Approval is bounded.** An approval applies only to its named mutation,
  repository, data plane, scope, and time. It never authorizes adjacent writes,
  bypassing validators, private-state access, or concealing a RED/degraded
  state. Record the approval and resulting receipt where the subsystem requires
  it.
- **Authorized advisory boundary.** Production Foundation V2.1 permits only
  the dedicated PIR read-only/advisory tables and bounded Agent event-store
  implementation described in tracked contracts. It does not authorize
  production PIR/Agent automation or any authority upgrade.
- **Local PostgreSQL exception.** An explicit task may operate one isolated
  AUTOSINT development/test PostgreSQL data plane bound only to
  `127.0.0.1:55432`: inspect documented variable names but not values; inspect
  installed runtimes; start/stop the isolated instance; create a dedicated new
  volume, development/test roles and databases; apply current migrations; run
  DB tests and synthetic backup/restore; and run release validation. It may not
  modify an unknown DB/volume, delete any DB/volume without separate exact
  reset approval, install system dependencies without separate approval, use
  production data/credentials, print passwords, or bind non-loopback.
- **Cleanup mutation.** Classify every tracked file and registered route before
  removal. Archive proven superseded material; delete tracked material only
  after deterministic reference checks prove it dead and replacement authority
  exists. Do not delete runtime artifacts, receipts, source data, DB contents,
  Evidence, or private operator history. An ignored-artifact retention policy
  is allowed; destructive cleanup needs separate exact approval.

## 7. UI truth rules

- **Read-only operator UI.** Default UI surfaces expose no browser-side
  POST/write/apply/import/promote/reset, OSIR bypass, commander-ready, scheduler,
  provider-enable, or other mutation control. There are no hidden write paths,
  and raw Evidence bodies do not appear in primary operator views.
- **Truthful state rendering.** UI/API views distinguish current data,
  retained/stale data, configured with no runtime data, blocked/login-required,
  DB/service unavailable, planned, gated-disabled, legacy-removed, and
  unverified states. HTTP 200 proves route availability only, not integration,
  current data, completeness, or communication. No-data and degraded states
  are first-class, not generic success or hidden exceptions.
- **Integration claims.** A capability is app-integrated only when current
  registered routes, shell navigation, canonical data source, rendered states,
  safe authority, focused tests, and honest current/no-data/degraded behavior
  all support the claim. Backend code, DB models, config, MCP tools, routes, or
  screenshots alone are insufficient.
- **Operator hierarchy.** Primary views answer what happened, where, why it
  matters, what changed, what is ready for RFI preview, what remains cue-only or
  missing, and what comes next. Raw IDs/JSON, long URL lists, debug counters,
  legacy linkage gaps, and detailed provenance belong in expandable audit
  sections.
- **Visual proof limit.** Screenshots support rendering only. UI reviews use
  scoped localhost/app windows, avoid unrelated desktop/private account state,
  identify route/title and screenshot/data timestamps, and compare rendered
  state with the same-source API when runtime truth is in scope.

## 8. Secrets/privacy

- **Never access or expose private material.** Do not read, print, request,
  copy, commit, upload, or place in reports: secrets, tokens, API keys,
  credentials, `.env` values, passwords, cookies, sessions, localStorage,
  sessionStorage, Chrome profiles, Keychain values, private browser/account
  state, private conversation IDs/URLs, DB dumps, raw Evidence bodies, or raw
  private conversation exports.
- **Public-only collection.** Do not bypass login, CAPTCHA, Cloudflare,
  paywall, session, access-control, or licensing boundaries. Credentialed
  collection requires explicit approval and approved providers; approved
  runtime credentials live only in ignored environment helpers and never in
  chat, tracked files, receipts, logs, screenshots, handoffs, or the mirror.
- **Minimum safe inspection.** Inspect documented environment-variable names,
  configuration keys, and capability state without reading values. Do not use
  private browser or account state to prove model availability, provider
  health, or runtime status.
- **Sanitized outputs.** Public mirrors and handoff packs exclude code secrets,
  DB files/volumes, backups containing real data, runtime artifacts/payloads,
  source catalogs unless approved, raw Evidence, inbox/staging/quarantine/latest,
  receipts/logs, screenshots, browser state, credentials, `.env`, generated
  ZIPs, and private local configuration backups.

## 9. Validation/release

- **Layered validation.** Validate structural/schema correctness, semantic
  completeness, raw-to-normalized preservation, normalized-to-API/UI
  traceability, current/retained/stale/no-data labeling, read-only/write-gated
  authority, implementation versus app integration, route availability versus
  current data, and storage/provenance versus actual communication separately.
- **Required checks.** Run focused tests for the changed area, `py_compile` for
  changed Python, syntax/schema/YAML/JSON checks as relevant, API/HTML route
  smoke for route work, `git diff --check`, privacy/secret and artifact scans,
  and `scripts/validate_release_surface.sh` when relevant and safe. Phase-level
  acceptance may also require full pytest, JS/import/OpenAPI checks,
  PostgreSQL migration/backup/restore, MCP handshake/gates, PIR/Agent/UI tests,
  documentation/archive consistency, and External Scout regression.
- **Natural proof.** Never claim External Scout `PROVEN` from tests, HTTP 200,
  one success, manual recovery/direct capture, screenshots, old packets, or a
  retained board. Use `scripts/report_external_scout_24_7_proof.py`; the
  default gate is three consecutive natural `:00 -> :28` prompt-to-async-
  harvester cycles, Live Board `stale=false`, active threads, no RED health,
  and no eval runtime hard-fails. Manual/direct actions are diagnostic only and
  do not count.
- **Release truth.** Keep acceptance, current runtime proof, and release
  readiness separate. If a required service is unavailable, report the exact
  environment blocker; do not start or mutate it without authorization and do
  not reclassify it as a code regression or cosmetic GREEN. Never claim
  `RELEASE_SURFACE_READY` unless the canonical validator emits it.
- **Checkpoints and reporting.** Every Production Foundation V2.1 phase writes
  a timestamped checkpoint under ignored
  `artifacts/operator_reading/latest/production_foundation_v2_1/`. Reports state
  objective/result, evidence timestamp, branch/HEAD/dirty scope, changed files,
  runtime/proof/release state, exact blocker, validation, route/data semantics,
  git/mirror status, privacy exclusions, remaining unproven work, and one safe
  next action. Do not overstate `PROVEN`, `GREEN`, `current`, app integration,
  communication, completeness, or commander-ready authority.

## 10. Git policy

- **Exact boundary.** Preserve unrelated changes. Inspect staged, unstaged, and
  untracked scope before and after work. Never use `git add .`; stage exact
  files or hunks only, and stop when mixed hunks cannot be separated safely.
- **Forbidden staging.** Never stage `.env*`, secrets, tokens, credentials,
  browser state/profiles, cookies/storage, DB files/volumes, real-data backups,
  `artifacts/*`, receipts, logs, screenshots, patch backups, runtime payloads,
  External Scout inbox/latest/staging/quarantine, raw Evidence, generated ZIPs,
  private config backups, or `docs/AUTOSINT_SOURCE_CATALOG.md` unless explicitly
  approved.
- **Autopush gate.** Automatic commit/push is allowed only when the exact task
  boundary is known, required validation passes, this constitution permits the
  mutation, no forbidden/unrelated file is staged, and the remote/branch target
  is clear. Stop on Plan/no-commit/no-push scope, failed validation, mixed or
  unclear diff, privacy risk, or an unapproved risky change to DB/schema,
  sources, apply/import, OSIR, commander-ready, Evidence, case links,
  credentials, browser private state, production models/prompts, or runtime
  lifecycle.
- **History safety.** No history rewrite, force-push, destructive reset, or
  remote-state mutation outside the task. Use conventional commits such as
  `feat`, `fix`, `chore`, `docs`, or `test`; use a feature branch/PR boundary
  for larger or risky work when appropriate. Push the current authorized
  branch only after the gate passes.
- **Git report.** State branch, commit hash, push result, exact committed files,
  validation/route smoke, final dirty state, ignored-artifact status, and
  explicit confirmation that no unauthorized DB, raw Evidence, case-link,
  source-config, OSIR, apply/import, secret, or private-browser mutation
  occurred.

## 11. Documentation lifecycle

- **Tracked authority.** Durable architecture, workflow, policy, safety, and
  workstream decisions belong in tracked docs/config/tests, not memory or a
  thread. Use current metadata/timestamps and explicitly record supersession and
  conflicts; old reports and the public mirror do not prove live runtime.
- **Read-first core.** The core bundle is
  `docs/status/AUTOSINT_CONTEXT_INDEX.md`,
  `docs/status/AUTOSINT_ASSISTANT_CONTEXT_CURRENT.md`,
  `docs/status/AUTOSINT_DOCUMENTATION_AUTHORITY.md`,
  `docs/status/AUTOSINT_DOCUMENTATION_INDEX.md`,
  `docs/status/AUTOSINT_DOCUMENTATION_CONFLICTS.md`,
  `docs/status/AUTOSINT_WORKSTREAMS.md`,
  `docs/status/AUTOSINT_SYSTEM_CONTRACT_CURRENT.md`,
  `docs/AUTOSINT_OPERATING_MODEL_CURRENT.md`,
  `docs/AUTOSINT_PRIMARY_WORKFLOW.md`, and
  `docs/AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md`.
- **Read-first specialized sources.** As relevant, read
  `docs/AUTOSINT_CHATGPT_PROJECT_OPERATING_MODEL.md`,
  `docs/AUTOSINT_LONG_RUNNING_WORK_MODEL.md`,
  `docs/AUTOSINT_ORCHESTRATION_ROADMAP.md`,
  `docs/AUTOSINT_SENSOR_ARCHITECTURE_V1.md`,
  `config/autosint_sensor_architecture.yml`,
  `docs/AUTOSINT_GLOBAL_SENSOR_COVERAGE_POLICY.md`,
  `docs/AUTOSINT_THEATER_WATCH_POLICY.md`,
  `docs/AUTOSINT_MARKET_PREDICTION_FINANCE_POLICY.md`,
  `docs/AUTOSINT_GPT56_MODEL_UPGRADE_EVALUATION.md`,
  `docs/AUTOSINT_EVALUATION_DATASET_V0.md`,
  `docs/AUTOSINT_CHATGPT_CODEX_HANDOFF_QUEUE.md`,
  `docs/AUTOSINT_CONTEXT_MIRROR_RUNBOOK.md`,
  `docs/AUTOSINT_LATTICE_INSPIRED_REFERENCE_ARCHITECTURE.md`,
  `config/autosint_workstreams.yml`, and
  `scripts/validate_release_surface.sh`, plus subsystem code/config/routes and
  focused tests named by the task.
- **Workstream report.** For status checks run
  `.venv/bin/python scripts/report_autosint_workstreams.py --dry-run --no-write`.
  Workstream rows are tracking/verification only and confer no mutation
  authority.
- **Archive discipline.** Classify tracked files/routes before cleanup. Move
  proven superseded material to tracked history with a manifest and updated
  links; delete only `DEAD_CONFIRMED` material with deterministic reference
  evidence and replacement authority. Preserve provenance and never delete
  ignored runtime history as part of tracked cleanup.
- **Context mirror.** After meaningful committed changes to architecture,
  workflow, validation, operator behavior, or this constitution, run the mirror
  publisher dry-run and publish only committed sanitized docs/config summaries
  after the private push. Commit/push the mirror separately after sanitization
  and consistency checks; it never proves current local runtime.
- **Constitution migration.** `AGENTS_RULE_INVENTORY.csv`,
  `AGENTS_RULE_MIGRATION.csv`, and `AGENTS_CONSTITUTION_REVIEW.md` record the
  legacy-to-constitution mapping. The deterministic checker must pass before
  claiming no durable rule was lost.

## 12. Stop conditions

Stop, preserve evidence, classify the blocker, and request the smallest needed
approval or report one bounded next action when any of these occurs:

- the repository, branch, task boundary, target, authority, remote, or
  snapshot identity is wrong, mixed, ambiguous, or conflicts with newer
  field-specific evidence;
- unrelated changes or inseparable mixed hunks appear, forbidden files/private
  data could be staged or exposed, or a secret/credential/private-state value
  would need to be read;
- validation fails, deterministic checks disagree, request/turn/contract
  identity mismatches, or a required receipt/proof/current-data source is
  absent; classify absence honestly instead of filling it from memory;
- a pending External Scout request exists, or the next step would require an
  unauthorized prompt, harvester, capture, recovery, retry, Chrome/browser,
  launchd, collector, scheduler, provider/API, or duplicate lifecycle action;
- the step would mutate an unknown DB/volume, production data, Evidence, case
  links, source configuration, OSIR, apply/import, commander-ready, proof
  history, rotation, or any gated PIR/Agent/MCP path without exact approval;
- the step would delete a DB/volume, runtime history, artifacts, receipts,
  source data, Evidence, or operator history, install dependencies, bind a
  service non-loopback, bypass access controls/validators, rewrite git history,
  or force-push without the separate required approval;
- a required environment/service/release gate is unavailable or RED. Report
  `KNOWN_OPERATOR_PAUSE_RED`, `UNKNOWN_RUNTIME_RED`,
  `PROOF_REBUILDING_NOT_COMPLETE`, or the exact environment blocker as
  applicable; do not conceal it or start services merely to clear the gate;
- this program unexpectedly changes current External Scout production
  behavior: stop with `CURRENT_EXTERNAL_SCOUT_RUNTIME_REGRESSION`.

Complexity, duration, prior failure, or an open research question is not itself
a stop condition. Continue methodically until success criteria pass or a real
condition above is reached.
