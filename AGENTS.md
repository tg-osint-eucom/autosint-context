# AUTOSINT Codex Instructions

These instructions are the durable repo-level operating rules for Codex work in AUTOSINT.

## Operating Principle

Work proof-first. Repo/runtime evidence wins over memory, prior chat summaries,
plans, or external review text. Before making current-state claims, inspect the
real code, tracked docs, route/API output, ignored receipt artifacts, launchd
state when relevant, tests, and release gates.

ChatGPT output is strategic input and candidate packet material, not ground
truth. AUTOSINT validation, quarantine, thread current-state selection, and
operator route behavior decide what is active.

## Active Repo And Legacy Checkouts

Primary clean AUTOSINT repo on this host:

```text
autosint-clean-20260621
```

Public sanitized context mirror worktree:

```text
autosint-context
```

Legacy/archive repo:

```text
autosintmvp
```

Use `autosintmvp` only when a task explicitly targets legacy/archive history.
Never use stale checkout `autOSINT` for current AUTOSINT work. Verify the
absolute local path with `pwd` before making changes, but do not publish
private local path strings into the public context mirror.

## Current Primary Surfaces

Primary operator routes:

- `/mission-control`
- `/external-scout/threads`
- `/havoc-rfi/SOCCENT`

Supporting/read-only routes:

- `/external-scout`
- `/api/v1/external-scout/live-case-board`
- `/api/v1/external-scout/threads`
- `/api/v1/havoc-rfi/SOCCENT`
- `/tsoc-havoc`
- canonical, evidence-passport, PIR, OSIR preview, agent, source-health, and
  audit routes when a task explicitly needs them.

Do not use `/dagrbook` as the primary browser surface. `/dagrbook`,
`/moltbook`, and `/control-plane` are removed legacy browser routes unless a
separate approved frontend thread restores them.

## Current Product Direction

AUTOSINT is a local-first External Scout and HAVOC/RFI operator review stack.
The External Scout Live Case Board is the current operator case board.

Core workflow:

```text
Mission Control -> External Scout Live Case Board -> TSOC/HAVOC -> HAVOC/RFI -> future controlled approval
```

Current rules:

- ChatGPT packets are candidate input only.
- `/external-scout/threads` is durable case/thread memory.
- `/external-scout` is the latest active packet inbox/support view.
- HAVOC/RFI consumes External Scout thread-current state first, then falls back
  to validated packets only when thread state is unavailable.
- OSIR, Evidence writes, case-link writes, source-config changes,
  apply/import, and commander-ready promotion remain closed unless a future
  controlled approval path explicitly opens them.

## Source Of Truth Files

Inspect the relevant current source-of-truth files before architecture,
operator-surface, capture, or policy work:

- `AGENTS.md`
- `docs/AUTOSINT_OPERATING_MODEL_CURRENT.md`
- `docs/AUTOSINT_PRIMARY_WORKFLOW.md`
- `docs/AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md`
- `docs/AUTOSINT_CHATGPT_PROJECT_OPERATING_MODEL.md`
- `docs/AUTOSINT_GLOBAL_SENSOR_COVERAGE_POLICY.md`
- `docs/AUTOSINT_THEATER_WATCH_POLICY.md`
- `docs/AUTOSINT_MARKET_PREDICTION_FINANCE_POLICY.md`
- `docs/AUTOSINT_GPT56_MODEL_UPGRADE_EVALUATION.md`
- `docs/AUTOSINT_EVALUATION_DATASET_V0.md`
- `docs/AUTOSINT_CHATGPT_CODEX_HANDOFF_QUEUE.md`
- `docs/AUTOSINT_CONTEXT_MIRROR_RUNBOOK.md`
- `docs/status/AUTOSINT_WORKSTREAMS.md`
- `config/autosint_workstreams.yml`
- `scripts/validate_release_surface.sh`

For Evidence, Temporal, OSIR, PIR, source registry, or sensor work, also inspect
the relevant core/config files before editing. Preserve existing Evidence,
Temporal Guardian, OSIR, and sensor-registry discipline.

## Live Case Board And External Scout

External Scout capture/output rules:

- The ChatGPT Project is a workspace; AUTOSINT threads are case memory.
- The Packet/Daily Scout output must use strict JSON/Markdown and the current
  source/sensor coverage contract.
- Capture writes only ignored runtime artifacts: staging, inbox, quarantine,
  latest, receipts, and logs.
- Invalid or schema-drifted captures fail closed and do not update current
  active state.
- Lower-quality packets may append to timeline without replacing best current
  state.
- Generated artifacts stay under `artifacts/` and are not committed.

Live Case Board rules:

- Active threads come from latest valid packets and retained thread history.
- Stale tracked and archived threads must be visibly separated from current
  active threads.
- Operator paths must show what happened, what changed, why it matters,
  readiness, gaps, and next checks before audit details.
- Raw packet IDs, raw JSON, long URL dumps, debug counters, and legacy linkage
  gaps belong in collapsed audit/provenance sections.

## Global Sensor Coverage

No required source or sensor lane may be silently omitted. Every required lane
must report an explicit status such as:

- `Checked and found`
- `Checked and not found`
- `Candidate found, not imported`
- `Not checked`
- `Stale`
- `Blocked / login required`

Required coverage includes official/advisory, public news, social/public
reaction, traffic/movement, satellite/geospatial, weather/environment,
markets/finance, prediction markets, crypto/risk, defense-industrial markets,
shipping/logistics/insurance, and multilingual/regional context.

Market, crypto, prediction-market, social, and public-comment lanes are cue-only
and cannot independently prove closure, reopening, attribution, causality,
intent, insider activity, OSIR release, or commander-ready status.

## Theater Watch

External Scout output may emit up to five active packets per cycle, but
`theater_watch_summary` must account for all required theaters:

- SOCCENT
- SOCEUR
- SOCPAC
- SOCAFRICA
- SOCSOUTH
- SOCKOR
- SOCOMD

Overflow or omitted candidate cases must have clear reasons, checked source
families or explicit unavailable/not-reported status, and next checks. Do not
let overflow candidates replace active thread state unless a valid packet is
emitted and promoted.

## Market / Prediction / Finance Enrichment

The following lanes must be explicit for active threads when market/prediction
finance enrichment is in scope:

- Polymarket
- Kalshi
- other public prediction markets
- broad market
- oil / energy
- shipping / tanker
- defense large-cap
- defense mid/small
- foreign defense stocks where represented
- regional markets
- insurance / freight / rates
- crypto / risk

These lanes remain cue-only. They may support HAVOC/RFI preview context, but
they do not create Evidence, case links, source-config changes, OSIR release,
apply/import, or commander-ready status.

## Model Upgrade Evaluation

Model announcements and ChatGPT/Codex review text are product input, not
AUTOSINT runtime truth. The current model-upgrade evaluation source of truth is
`docs/AUTOSINT_GPT56_MODEL_UPGRADE_EVALUATION.md`.

Do not change production prompts, External Scout capture behavior, validator
authority, Live Case Board readiness, HAVOC/RFI selection, or scheduled model
defaults for a new model family until a non-production replay has proven:

- actual model availability in the intended ChatGPT, Codex, or API surface;
- strict packet validation with required coverage matrices and cue-only
  language;
- no DB, Evidence, case-link, source-config, OSIR, apply/import,
  commander-ready, launchd, secret, or private-browser-state mutation;
- acceptable latency, reliability, and cost for the intended role.

Default role split for evaluation only: flagship models for hard Codex/root
cause/deep review, balanced models for routine non-production replay, and fast
low-cost models for helper summaries. Validators and route/report output remain
the authority.

## Evaluation Dataset And Handoff Queue

`docs/AUTOSINT_EVALUATION_DATASET_V0.md` and
`config/autosint_eval_grader_rules.yml` define deterministic local grading for
good/bad AUTOSINT behavior before model migration, fine-tuning, local-model
comparison, or automated handoff work. The dataset is sanitized evaluation
memory only; generated cases belong under ignored `artifacts/model_eval/`.

`docs/AUTOSINT_CHATGPT_CODEX_HANDOFF_QUEUE.md` defines the safe
ChatGPT-review-to-Codex handoff boundary. V0 is file-based and copy-safe only:
Codex may read sanitized files from the ignored handoff inbox and prepare a
paste-ready prompt, but must not scrape ChatGPT private URLs, read browser
state, use AppleScript/System Events, use the clipboard, or auto-post into
ChatGPT/Codex unless a future official non-private-state path is verified and
explicitly approved.

## Workstreams And Long-Running State

Use `config/autosint_workstreams.yml` and
`docs/status/AUTOSINT_WORKSTREAMS.md` for long-running AUTOSINT state. Do not
rely on chat memory alone for workstream status.

Run the workstream report for status checks:

```bash
.venv/bin/python scripts/report_autosint_workstreams.py --dry-run --no-write
```

Workstream tracking is project memory and verification only. It must not become
an apply/import, Evidence-write, case-link, source-config, OSIR, launchd, or
commander-ready action path.

## Context Mirror

The public `tg-osint-eucom/autosint-context` mirror is the durable sanitized
context handoff for ChatGPT/Codex when private connector access fails or context
is lost.

After meaningful private repo commits that change workflow, architecture,
validation status, operator behavior, or repo-level instructions, run:

```bash
.venv/bin/python scripts/publish_autosint_context_mirror.py --dry-run
.venv/bin/python scripts/publish_autosint_context_mirror.py --publish
```

The mirror must remain docs-only and sanitized: no code secrets, DB files,
runtime artifacts, raw Evidence, External Scout inbox/staging/quarantine/latest
payloads, receipts/logs, browser state, screenshots, credentials, tokens, or
`.env` values.

## Context And Memory Source Of Truth

Codex memories are helpful recall only. They can speed up orientation, but they
are not the AUTOSINT source of truth and must not override repo/runtime
evidence, `AGENTS.md`, tracked docs, tests, launchd state, receipts, route
responses, or release gates.

Durable operating rules must live in this file or another tracked AUTOSINT doc.
The current Codex/ChatGPT thread is temporary working context only.

For substantial multi-step AUTOSINT work, use `/goal` so the objective,
verification gates, and stop conditions survive long-running turns.

Codex memories should be enabled for helper recall when available:

```toml
[features]
memories = true
```

After meaningful commits that change workflow, architecture, validation status,
or operator behavior, refresh the public `autosint-context` mirror after the
private repo push.

## Evidence, Temporal, OSIR, And Sensor Discipline

Never mutate raw Evidence rows to make UI cleaner. Search/discovery results are
not Evidence until a future explicit approval/import path validates and accepts
them.

Temporal validation belongs to the Temporal Guardian policy and code. Do not
hardcode freshness or TTL behavior into unrelated collectors or UI code.

OSIR export safety remains policy-gated. Do not bypass OSIR blockers or open
commander-ready gates from review surfaces.

Sensor/source work must preserve public-only collection unless credentialed
collection is explicitly approved. Do not bypass CAPTCHA, Cloudflare, login
walls, paywalls, private/session-only pages, cookies, browser localStorage, or
private browser state.

## Operator Surface Discipline

Browser/UI surfaces must remain read-only:

- no browser-side POST/write/apply/import/promote/reset controls unless a task
  explicitly designs an approved controlled path;
- no hidden mutation paths;
- no OSIR bypass controls;
- no commander-ready controls;
- no raw Evidence content dumps in main operator paths.

Operator-facing language should answer:

- What happened?
- Where?
- Why it matters?
- What changed?
- What is ready for HAVOC/RFI preview?
- What remains cue-only or missing?
- What next?

## AUTOSINT Standing Autopush Policy

Codex may stage, commit, and push automatically after implementation when the autopush gate passes.

Codex must stop and ask the user when:

- the task explicitly says no commit, no push, or Plan Mode;
- validation fails;
- the diff boundary is mixed or unclear;
- unrelated files appear;
- forbidden files appear;
- secrets or private data might be involved;
- DB/schema/source-config/OSIR/apply/import behavior changes without explicit approval;
- remote/branch/push target is unclear.

### Autopush Gate

Before staging, Codex must confirm:

1. Boundary is clean.

   - Staged files must match the task scope exactly.
   - Do not use `git add .`.
   - Use hunk staging when needed.
   - Stop if unrelated files or mixed hunks cannot be separated safely.

2. Validation is green.

   Required by default:

   - `git diff --check`
   - targeted pytest for changed area
   - `py_compile` for changed Python files
   - release surface validation when available or requested

3. Forbidden files are not staged.

   Never stage or push:

   - `.env` or `.env.*`
   - secrets
   - tokens
   - credential files
   - browser profile files
   - cookies
   - localStorage/sessionStorage
   - DB files
   - `artifacts/*`
   - screenshots
   - logs
   - patch backups
   - External Scout inbox/latest/staging/quarantine/receipts/logs
   - `docs/AUTOSINT_SOURCE_CATALOG.md` unless explicitly approved

4. Risky mutation classes require explicit approval.

   Stop before commit/push if the task changes:

   - DB schema/migrations
   - source registry/config
   - apply/import path
   - OSIR gate behavior
   - commander-ready promotion
   - Evidence writes
   - case-link writes
   - credential handling
   - browser private-state access

5. Final report must include:

   - branch
   - commit hash
   - push result
   - files committed
   - validation summary
   - route smoke summary if applicable
   - current dirty state
   - confirmation no DB mutation
   - confirmation no raw Evidence mutation
   - confirmation no case-link mutation
   - confirmation no source-config mutation
   - confirmation no OSIR bypass
   - confirmation no apply/import path
   - confirmation generated artifacts remained ignored/uncommitted
   - confirmation `docs/AUTOSINT_SOURCE_CATALOG.md` remained untouched/untracked unless explicitly approved
   - confirmation no secrets/private browser state were read or printed

### Push Behavior

If the current repo is the clean AUTOSINT repo and the gate passes:

- commit with a conventional commit message;
- push the current branch to origin.

For larger or risky features:

- use a feature branch if appropriate;
- push branch;
- report PR/opening instructions if available.

Conventional commit examples:

- `feat(...)`
- `fix(...)`
- `chore(...)`
- `docs(...)`
- `test(...)`
