# AUTOSINT External Scout Runbook

External Scout is the preferred external public-information input layer for AUTOSINT. ChatGPT produces structured public candidate packets; AUTOSINT captures, validates, quality-checks, and previews them. Packets remain candidate input only until a future explicit approval path imports selected source URLs.

## ChatGPT Project

Project name:

```text
AUTOSINT External Scout
```

ChatGPT Project operating model:

- AUTOSINT Live Case Board threads are case memory.
- ChatGPT Project chats are workspaces only.
- `AUTOSINT Daily External Scout` is the scheduled machine-output chat and
  must produce strict JSON/Markdown only.
- `AUTOSINT System Control` is the human/admin chat for Codex tasks, GitHub,
  launchd, prompt updates, architecture, debugging, and roadmap work.
- Optional `CASE - <topic>` chats are human-created deep dives only. Do not
  auto-create one per packet, thread, or capture.
- Case deep-dive chats must start from AUTOSINT thread data and are not
  Evidence or source of truth.

See `docs/AUTOSINT_CHATGPT_PROJECT_OPERATING_MODEL.md`.

The Project Instructions should require:

- Event-centric case packets.
- Facts first, source relationships second, system status third.
- Up to five active candidate packets by default. If more credible cases exist,
  the extra cases go into top-level `overflow_candidate_cases` with an omitted
  reason and next check.
- A top-level `theater_watch_summary` covering SOCCENT, SOCEUR, SOCPAC,
  SOCAFRICA, SOCSOUTH, SOCKOR, and SOCOMD, even when a theater has no active
  packet.
- The required source/sensor coverage lanes:
  - Official / Advisory
  - Public News
  - Social OSINT
  - Traffic / Movement
  - Satellite / Geospatial
  - Weather / Environment
  - Markets / Finance
  - Prediction Markets
  - Crypto / Risk Sentiment
  - Defense-Industrial Markets
  - Shipping / Logistics / Insurance
  - Multilingual / Regional Media
  - Public Comments / Reaction
- Exact source-family status values:
  - Checked and found
  - Checked and not found
  - Candidate found, not imported
  - Not checked
  - Stale
  - Blocked / login required
- Separation of claim, counter-claim, observed, advisory, context, and missing.
- Operator fields: `operator_bluf`, `what_changed`, `so_what`, `source_relationships`, `decision`, `collection_plan`, `system_status`, `audit_notes`, and `quality_self_check`.
- Source quality fields: `strong_sources`, `weak_sources`,
  `missing_source_lanes`, `cue_only_lanes`, and
  `next_collection_priority`, plus optional source quality scores when useful.
- `commander_ready=false` and `mutation_performed=false`.
- No private data, cookies, sessions, tokens, browser storage, credential files, login-wall bypass, CAPTCHA bypass, or paywall bypass.

See `docs/AUTOSINT_GLOBAL_SENSOR_COVERAGE_POLICY.md` and
`docs/AUTOSINT_THEATER_WATCH_POLICY.md` for the durable coverage and theater
watch contract.

## Generation And Capture Timing

Target desired upstream:

```text
ChatGPT Scheduled Task generates strict output hourly.
AUTOSINT capture validates the exact configured Scheduled Task output
conversation at :08.
```

The Scheduled Task production path is the preferred upstream generator once it
is proven. AUTOSINT remains authoritative: capture, staging, validation,
quarantine, active inbox selection, Live Case Board freshness, health monitor,
and eval decide whether output becomes current. ChatGPT Scheduled Task output
is candidate material only, not Evidence, not OSIR, and not commander-ready.
If ChatGPT routes Scheduled Task output into a dedicated task-result
conversation instead of the Packet chat, do not overwrite the working Packet
capture target during proof. Put the task-result conversation id in ignored
`artifacts/external_scout/scheduled_task_capture_target.json` and probe it
with `scripts/probe_external_scout_scheduled_task_capture.py`. Keep local
fallback prompt submission pointed at the Packet chat through ignored
`artifacts/external_scout/prompt_trigger_target.json`.

Current proven production upstream remains the local Packet-chat prompt
trigger, but the Pro Extended contract is now Scout Findings, not direct
strict packets. The hourly wrapper defaults to
`--scout-findings-mode`: ChatGPT may emit a downloadable
`autosint_scout_findings_YYYYMMDDTHHMMSSZ.json` file with real source checks,
and AUTOSINT fetches that visible attachment, normalizes it with
`scripts/normalize_external_scout_findings_to_packets.py`, validates the strict
packet candidate, applies the newer-than-inbox guard, and promotes only when
`validation_error_count=0`. Receipts must record
`normalized_promoted_to_inbox`, `normalized_validation_error_count`,
`scout_findings_attachment_filename` when an attachment is used, and the usual
no-DB/no-Evidence/no-OSIR/no-commander-ready safety flags. Set
`AUTOSINT_PROMPT_TRIGGER_SCOUT_FINDINGS_MODE=0` only for explicit strict-packet
fallback work.

### Async Scout Findings Harvester

Pro Extended can take longer than a bounded prompt-trigger readiness window.
In Scout Findings mode, the prompt-trigger is submit-only by default: once the
exact Packet target is verified, the user turn is verified, generation starts,
and a pending request is written, the wrapper exits instead of polling the
renderer for ready output. This keeps the Chrome renderer, launchd job, and
prompt-trigger lock from being held for the full Pro Extended generation. The
pending request is written here:

```text
artifacts/external_scout/pending_generation/latest_pending_request.json
```

The pending receipt records the trigger request id, redacted Packet target,
freshness deadline, prompt receipt path, and safety flags. It must not include
cookies, sessions, localStorage/sessionStorage, Chrome profile data, credential
values, raw Evidence, DB dumps, or private browser state.

The async harvester checks the same configured Packet target without sending a
new prompt:

```bash
.venv/bin/python scripts/harvest_external_scout_findings.py --once
```

If a matching visible `autosint_scout_findings_*.json` attachment or visible
Scout Findings JSON is found for the pending `trigger_request_id`, the
harvester saves the source findings under ignored artifacts, runs
`scripts/normalize_external_scout_findings_to_packets.py`, and promotes only
when `validation_error_count=0`, the packet is newer than inbox, and the
finding is still within freshness. If findings are absent, stale, not newer
than inbox, or have a trigger id mismatch, the harvester writes a receipt and
does not promote.

Wrapper and LaunchAgent template:

```text
scripts/run_external_scout_findings_harvester_once.sh
launchd/com.autosint.external-scout-findings-harvester.plist
```

### Packet v2 Async Renderer Hygiene

Packet v2 Pro Extended Scout Findings generation must not keep the prompt
trigger attached to one busy renderer while the model thinks. For normalized
Scout Findings mode, the wrapper now defaults to:

```text
AUTOSINT_PACKET_RELEASE_AFTER_SUBMIT=1
AUTOSINT_PACKET_REOPEN_FOR_HARVEST=1
AUTOSINT_PACKET_KEEP_OPEN_THROUGH_CAPTURE=0
```

The prompt-trigger command also uses `--scout-findings-submit-only` in Scout
Findings mode. If exact-tab release is unsafe or skipped, the wrapper still
exits after pending-request recording; the harvester owns delayed extraction.
The prompt-trigger may release only the exact configured Packet v2 tab after
all of these gates are true: the target conversation id matched, the user turn
was verified, generation started, the composer was known cleared, and the
pending request was written. Existing pending state still blocks duplicate
prompts.

The harvester reopens the exact configured target URL or reconstructs a
`chatgpt.com/c/<conversation_id>` fallback, then revalidates the target before
extracting visible Scout Findings JSON or an `autosint_scout_findings_*.json`
attachment. If findings are still absent, the harvester can release the exact
tab again after confirming the composer is empty. If a normalized promotion
succeeds and the capture/proof window still needs the tab, it records
`kept_open_for_capture_window=true` instead of closing the tab.

Receipts record `tab_released_after_submit`, `pending_request_written_before_release`,
`reopened_for_harvest`, `harvest_target_revalidated`,
`kept_open_for_capture_window`, `tab_released_after_capture`, and
`release_skipped_reason`. The lifecycle never closes all Chrome windows, never
creates a new ChatGPT conversation, never sends a duplicate prompt while a
pending request is active, and never reads cookies, storage, Chrome profile
files, credentials, raw Evidence, or DB contents.

#### Packet v2 Page Unresponsive Recovery

Observed working recovery on 2026-07-06:

1. Treat a visible Chrome `Page Unresponsive` dialog for the exact Packet v2
   tab as a renderer-blocked state, not a validator or provider failure.
2. Take a visible screenshot first and inspect current receipts before
   interacting with Chrome.
3. Confirm the pending request is the same Packet v2 turn; do not send a new
   prompt and do not create a new chat.
4. Click `Wait` once on the `Page Unresponsive` dialog.
5. If the dialog repeats or harvester/capture still reports
   `applescript_timeout:external_scout_harvest_readiness_probe`, click
   `Exit Page` only for the exact configured Packet v2 tab.
6. Immediately renavigate that same tab to the exact configured Packet v2 URL
   from `artifacts/external_scout/capture_target.json`.
7. Verify the target conversation id still matches, the visible ChatGPT UI
   loads past browser checks, and no new prompt was submitted. After opening
   or renavigating the Packet v2 URL, wait for the page to stabilize before
   probing it; do not immediately run JS extraction against a still-loading or
   spinner-only ChatGPT surface.
8. Let the existing harvester/capture path collect the already-generated Scout
   Findings JSON or `autosint_scout_findings_*.json` attachment.
9. Promote only through the normal validator gate:
   `normalized_validation_error_count=0`, newer than inbox, matching
   `trigger_request_id`.

Operator discipline for this URL: announce each completed step (`opened`,
`loaded`, `target matched`, `composer safe`, `Wait clicked`,
`Exit Page clicked`, `renavigated`, `harvest/capture receipt written`) before
moving to the next one. This is especially important for
`https://chatgpt.com/g/g-p-6a371bc30550819186bc75d0f5c02dd7/c/6a466c59-1774-83e8-ba01-86406d8922b9`.

This recovery produced the first successful `:30 -> :00` Pro Extended async
cycle on 2026-07-06: prompt receipt `20260706T153008Z`, Scout Findings
`generated_at=2026-07-06T15:38:33Z`, harvester/capture receipt
`20260706T155941Z`, `validation_error_count=0`, and five packets promoted.
The recovery used visible UI only and did not read cookies, sessions,
localStorage/sessionStorage, Chrome profile files, credentials, raw Evidence,
DB contents, or private browser state.

Load/start the LaunchAgent only after a successful normalized recovery proof
and explicit operator approval. On production hosts where it is already loaded,
verify receipts and health before counting natural-cycle proof. Otherwise, run
it manually for bounded checks or leave it as a staged production template.

On 2026-06-28, the existing `AUTOSINT Daily External Scout` Scheduled
Task was updated with the strict self-contained prompt and resumed, but the
proof run was not capturable: the Scheduled Tasks page showed `Выполняется`
for more than ten minutes, exposed no run-now control, no output/result chat
link, and no readable task-associated output conversation, and the Packet chat
did not advance before the natural `:08` capture. Capture receipt
`20260628T190806Z_capture_receipt.json` correctly selected the Packet chat but
safe-skipped `older_than_latest_inbox` against generated_at
`2026-06-28T17:50:30Z`. The local fallback prompt trigger was restored and
receipt `20260628T192327Z_prompt_trigger_receipt.json` produced a fresh strict
Packet-chat response with `validation_error_count=0`; capture receipt
`20260628T193810Z_capture_receipt.json` promoted five packets generated_at
`2026-06-28T19:24:32Z` and returned the Live Board to `stale=false`.

Later in the same session, ChatGPT exposed an outside-project task-result conversation
`4 new candidate packets emitted for review`
(`.../c/6a4179c7-3460-83e8-80a8-3a6087319e50`) with generated_at
`2026-06-28T19:34:28Z`, but a dry-run capture against that exact conversation
found `packet_count=4`, `valid_packet_count=0`, and
`validation_error_count=12` because `source_relationships` buckets such as
`claim`, `counter_claim`, and `context` were strings instead of arrays. The
ignored live Scheduled Task prompt artifact was tightened to require array
buckets, and the live task prompt was updated through the visible Scheduled
Tasks UI. The next observed Scheduled Task run still remained visible as
`Выполняется` after the local Packet fallback had already generated
generated_at `2026-06-28T20:06:30Z`; capture receipt
`20260628T200809Z_capture_receipt.json` promoted five Packet-chat packets with
`validation_error_count=0`. A scheduled-task probe against the exact task
result conversation then found a strict-valid Scheduled Task packet set
generated_at `2026-06-28T20:05:53Z` with `packet_count=5` and
`validation_error_count=0`, but it correctly did not promote because the Packet
fallback inbox was already newer. The user deleted that outside-project
conversation; it must not be treated as the AUTOSINT Project Packet target.
The Scheduled Tasks page was then rechecked through the visible UI and showed
`AUTOSINT Daily External Scout` as `Приостановлено · Последний запуск Сегодня`.
The task editor was opened read-only after the outside-project result chat was
deleted; it exposed only task title, instructions, hourly repeat interval, and
end time controls, with no visible output chat, Project, or conversation target
selector. The task actions menu exposed `Запустить сейчас` and `Открыть чат`,
but the `Открыть чат` control did not expose a URL or target in the DOM; do not
click it automatically because it may reopen or navigate to an outside-project
task-result chat.
After explicit approval, `Открыть чат` was clicked read-only and navigated to
`https://chatgpt.com/` with no conversation id, no `candidate_packets`, no
`generated_at`, and no task output. Treat the existing Scheduled Task as
orphaned/unusable for production capture until ChatGPT exposes or creates a
Project-scoped task output conversation.
Keep it paused until a Project-scoped output path is available; do not resume
it if it will create outside-project `chatgpt.com/c/...` result chats.
This confirms the current bottleneck is
upstream competition and target/timing, not the Packet-chat capture bridge:
Scheduled Task output can become valid, but it is not production-primary while
the local prompt trigger is also generating a newer packet before capture.

Do not demote or disable the local Packet-chat prompt trigger again until a
Scheduled Task output chat is proven capturable and two natural Scheduled Task
output -> capture cycles pass. If ChatGPT Scheduled Tasks cannot expose a
stable readable output conversation, keep them as unverified product input and
continue using the local prompt-trigger loop as the production upstream.

Current async local fallback timing:

```text
Prompt trigger every hour at :30.
Scout Findings harvester checks every 5 minutes.
Capture every hour at :00.
```

The local prompt trigger posts the Scout Findings prompt to the visible Packet
chat, records `scout_findings_pending`, and exits after verified generation
start. It is fallback, not the desired Scheduled Task primary path. The async
harvester reopens the exact Packet target, extracts matching Scout Findings
when ready, normalizes and promotes validator-clean packets, and capture safely
skips when the normalized packet is already in the inbox.

## Runtime Adapter Environment

External Scout wrappers load one optional ignored runtime environment file:

```text
artifacts/external_scout/runtime_env.sh
```

This file is for local runtime names only and must never be committed or
printed. The wrappers log only whether the file was loaded, not any values.

Use this path for read-only adapter credentials such as Kalshi, OpenSky,
Global Fishing Watch, or NASA FIRMS when approved:

```bash
export AUTOSINT_KALSHI_CREDENTIALS_ENABLED=1
export KALSHI_API_KEY_ID=...
export KALSHI_API_PRIVATE_KEY_PEM='...'
export OPENSKY_CLIENT_ID=...
export OPENSKY_CLIENT_SECRET=...
export GFW_API_TOKEN=...
export NASA_FIRMS_MAP_KEY=...
export FMP_API_KEY=...
export TELEGRAM_API_ID=...
export TELEGRAM_API_HASH=...
export AUTOSINT_TELEGRAM_CHANNELS=real_DonaldJTrump,V_Zelenskiy_official
```

Alternative accepted names are `KALSHI_ACCESS_KEY` or `KALSHI_API_KEY` for the
key id and `KALSHI_PRIVATE_KEY_PEM` for the private key. Do not put browser
cookies, browser sessions, Chrome profile paths, localStorage/sessionStorage,
or personal web-login state in this file.

To create that ignored file without printing credential values, use the helper
and enter values interactively:

```bash
.venv/bin/python scripts/configure_external_scout_runtime_env.py
.venv/bin/python scripts/check_external_scout_runtime_env.py
```

The helper writes only the ignored runtime env file, sets file mode `0600`, and
reports only env-name presence. It must not be used to ingest browser cookies,
sessions, Chrome profiles, localStorage/sessionStorage, `.env` dumps, or
credential files. After the checker reports the required Kalshi env names are
visible, run post-capture enrichment or wait for the next capture wrapper.

A pinned logged-in Kalshi browser tab is allowed for human review only.
AUTOSINT 24/7 enrichment must use public/API adapters and must not read browser
cookies, sessions, localStorage/sessionStorage, or Chrome profile state.
Telegram public channel pages may be checked through ordinary public `t.me`
GET requests. For more stable public-channel reads, the approved Telethon path
uses `TELEGRAM_API_ID`, `TELEGRAM_API_HASH`, approved channel names, and an
ignored local session file under `artifacts/telegram/`. It must not use browser
cookies, logged-in tabs, localStorage/sessionStorage, Chrome profile files, or
private browser state.
Financial Modeling Prep (`FMP_API_KEY`) may be used for read-only
market/finance quote and profile checks. These market/finance rows remain
cue-only and cannot prove event causality, attribution, or commander-ready
status.

To verify runtime visibility without reading or printing credential values:

```bash
.venv/bin/python scripts/check_external_scout_runtime_env.py
```

The checker reports only file presence and env-name presence. It never prints
credential values and does not read browser private state.

## Provider Decision Rules

Provider/source status on `/external-scout/24-7` follows the durable Sensor
Architecture v1 contract in `docs/AUTOSINT_SENSOR_ARCHITECTURE_V1.md` and
`config/autosint_sensor_architecture.yml`. Source URL status is separate from
adapter health:

- Polymarket and Manifold are public API lanes and do not need keys.
- Kalshi, Global Fishing Watch, OpenSky, and Financial Modeling Prep are
  configured read-only adapters when their ignored runtime env names are
  present; display only presence/status, never values.
- Telegram public `t.me` pages can be public-web checked. Approved Telethon
  public-channel reads are configured when `TELEGRAM_API_ID`,
  `TELEGRAM_API_HASH`, approved channels, and the ignored local session file are
  present; show presence/status only, never credential values.
- NASA FIRMS remains optional/unresolved unless `NASA_FIRMS_MAP_KEY` is present
  and smoke passes.
- Licensed news, X/Twitter API, Reddit API, arbitrary Telegram scraping,
  translation/search API, paid AIS/freight/satellite, Polygon/Massive, and
  similar paid/restricted sources are architecture references, not current
  blockers unless a current active case requires them and public/configured
  alternatives cannot satisfy the lane.

Prompt artifacts and live ChatGPT Project Instructions must include Provider
Decision Rules, Required Theater Watch, Required Source Search Itinerary,
top-level `trigger_request_id` when provided, `scheduled_task_run_id` when
scheduled, `generated_at`, `candidate_packets`, `theater_watch_summary`,
`overflow_candidate_cases`, `insurance_freight_rates`, cue-only boundaries, and
the no-private-state rule. Do not regress to a JSON-only
`{"candidate_packets":[...]}` contract.

## Source URL Inventory

After a successful capture and post-capture enrichment, the wrapper refreshes a
read-only candidate source URL inventory and public candidate-source
verification:

```bash
.venv/bin/python scripts/build_external_scout_source_url_inventory.py
.venv/bin/python scripts/verify_external_scout_candidate_sources.py --include-history --limit 220 --timeout 3 --max-seconds 240
```

Verification intentionally includes current plus stale/retained candidate URLs
so the pinned `/external-scout/24-7` page can show provider/source health for
active cases and retained continuity cases from the same canonical proof
report. Current URLs are prioritized before stale/retained and history-only
URLs, and the wall-clock budget prevents this diagnostic pass from becoming an
unbounded capture blocker.

Generated outputs:

```text
artifacts/source_coverage/latest/all_source_urls.json
artifacts/source_coverage/latest/all_source_urls.md
artifacts/source_coverage/latest/candidate_source_verification.json
artifacts/source_coverage/latest/candidate_source_verification.md
```

This inventory and verification output are local candidate memory for dedupe,
operator review, and source-gap triage only. They do not import Evidence, create
case links, mutate source config, open OSIR, perform apply/import, change
commander-ready state, use browser cookies/sessions, read Chrome profile state,
bypass login/CAPTCHA/paywalls, or print credential values. Candidate URLs can
still appear as follow-up gaps until a read-only adapter or approved import path
turns the lane into an explicit checked source.

When a deterministic read-only adapter checks a candidate URL, it may write
`source_gap_closure_notes` into a supplemental External Scout packet. Those
notes close only the specific `source_area` / `lane` they name, remain
review-only provenance, and do not create Evidence, case links, source-config
state, OSIR release, apply/import action, or commander-ready status.

## 24/7 Proof Loop

Do not call External Scout 24/7-ready after a single green run. The production
loop is considered proven only after repeated natural cycles leave durable
proof artifacts.

Use the read-only proof reporter:

```bash
.venv/bin/python scripts/report_external_scout_24_7_proof.py --dry-run
```

Operator browser surface:

```text
/external-scout/24-7
/api/v1/external-scout/24-7-proof
```

Keep `/external-scout/24-7` as the single pinned External Scout operator tab.
It reads prompt-trigger receipts, capture receipts, current health, Live Board
state, current/stale case health, source gaps, enrichment gates, logs, and the
existing eval summary through the same canonical proof report builder as
`/api/v1/external-scout/24-7-proof`. `/external-scout/threads`, HAVOC/RFI, JSON,
logs, and artifacts are read-only drill-downs or verification views, not
separate control sites. No additional app server is required. The proof script
writes generated reports only under ignored `artifacts/external_scout/24_7_proof/latest/`
unless `--no-write` is passed.

Default pass criteria:

- three consecutive natural async cycles are schedule-aligned from prompt to
  harvester to capture;
- each cycle has prompt submitted, user turn verified, request-id visibility,
  `scout_findings_pending=true`, and no duplicate prompt while pending;
- the harvester finds matching Scout Findings or an attachment, runs the
  normalizer, and records `normalized_validation_error_count=0`;
- capture either promotes or safely skips an equivalent already-ingested packet
  with validation errors equal zero;
- current health is not `RED`;
- Live Board is `stale=false`;
- active thread count is greater than zero;
- eval current-runtime hard-fails are absent.

If any cycle fails, record the exact blocker, use the bounded recovery playbook
only when health is `RED` or the board is stale/zero-active, and restart the
consecutive natural-cycle proof count after the fix.

Do not mark Scheduled Tasks production-ready until two natural Scheduled Task
output cycles have generated fresh strict packets in the exact configured
Scheduled Task output conversation, capture has promoted or safely skipped
equivalent strict packets with `validation_error_count=0`, Live Board has
stayed `stale=false`, and eval has no current-runtime hard-fails.

Scheduled Task probe command:

```bash
.venv/bin/python scripts/probe_external_scout_scheduled_task_capture.py
```

The probe reads ignored
`artifacts/external_scout/scheduled_task_capture_target.json`, runs an
External Scout capture dry-run with `--require-target`, writes a probe receipt
under ignored `artifacts/external_scout/scheduled_task_probe_receipts/`, and
does not promote unless `--promote-if-valid` is explicitly passed and the
dry-run finds a new target-matching packet set with `validation_error_count=0`.
Use this for delayed Scheduled Task proof; keep the normal
`artifacts/external_scout/capture_target.json` pointed at the Packet chat until
the Scheduled Task path has two proven natural cycles.
By default, the probe rejects non-project `https://chatgpt.com/c/...` result
URLs; production proof must use a ChatGPT Project URL such as
`https://chatgpt.com/g/.../c/...` or the canonical Project Packet chat.
If the Scheduled Task UI can only emit outside-project result chats, leave it
paused and continue using the local Project Packet-chat trigger/capture loop.

For a clean Scheduled Task proof window, pause or unload only the local
`com.autosint.external-scout-prompt-trigger` fallback if explicitly needed,
leave `com.autosint.external-scout-capture` and
`com.autosint.external-scout-health-monitor` alone, and restore the fallback if
the Scheduled Task output is late, stuck, missing, or schema-invalid.

If the existing Scheduled Task cannot be safely resumed, edited, or opened to a
Project-scoped output chat, do not use it as production upstream. Create or
replace a Scheduled Task only if the replacement can be proven to write to a
Project-scoped task output chat; do not create duplicate tasks by default and
do not create automatic per-case chats.
If a human explicitly wants to inspect the associated task chat, use the
visible `Открыть чат` menu action in the Scheduled Tasks UI as a read-only
handoff step and verify the resulting URL is Project-scoped before configuring
`scheduled_task_capture_target.json`.

After the existing task was proven orphaned, a replacement creation request was
submitted from the canonical Project Packet chat with the full self-contained
strict Scheduled Task prompt and a hard guard: create the replacement only if it
can remain associated with the current AUTOSINT External Scout Project /
Packet conversation. ChatGPT returned exactly
`TASK_CREATION_BLOCKED_PROJECT_OUTPUT_UNAVAILABLE`. This confirms the current
ChatGPT UI/Tasks capability cannot create the required Project-scoped Scheduled
Task output path from the Packet chat. Keep the local Packet-chat prompt trigger
as the production upstream until ChatGPT exposes a Project-scoped Scheduled Task
output conversation.

On 2026-06-28 a fallback prompt trigger exposed a wrong-window foreground
drift: metadata selected the Packet chat, but JavaScript could run in a
non-target ChatGPT window after Chrome window reordering. The recovery patch
requires prompt/capture target scripts to revalidate the foreground Packet tab
before executing JavaScript. Receipt `20260628T174230Z_prompt_trigger_receipt.json`
then proved Packet-chat request-id delivery with
`strict_packet_validation_error_count=0`; capture receipt
`20260628T175854Z_capture_receipt.json` promoted four valid packets generated_at
`2026-06-28T17:50:30Z` and restored Live Board `stale=false`.

Do not install or load launchd until manual dry-run and real one-shot capture
are consistently valid. On 2026-07-02, Packet v2 with Pro Extended produced
`autosint_scout_findings_20260702T174610Z.json`; the normalizer dry-run and
promotion produced five validator-clean packets generated_at
`2026-07-02T17:46:10Z`, Live Board `stale=false`, and health `WARN` only for
paused prompt-trigger/source-lane warnings. Restart prompt-trigger only after
this normalized path is intentionally used by the wrapper; keep Scheduled
Tasks paused.

The installed External Scout LaunchAgents should rely on the wrapper scripts'
timestamped logs under ignored `artifacts/external_scout/*_logs/`. Avoid
`StandardOutPath` / `StandardErrorPath` entries in the LaunchAgent plists for
these jobs; on 2026-06-27 those unused launchd stdout/stderr paths caused
pre-exec `EX_CONFIG` failures before the wrapper could start. The local repair
removed those keys, reloaded only:

- `com.autosint.external-scout-prompt-trigger`
- `com.autosint.external-scout-capture`

Post-repair launchd kickstart proof wrote prompt receipt
`20260627T015843Z_prompt_trigger_receipt.json` with
`packet_ready_for_capture=true`, `strict_packet_validation_error_count=0`, and
generated_at `2026-06-27T02:00:00Z`; capture receipt
`20260627T021023Z_capture_receipt.json` promoted five valid packets with
`validation_error_count=0` and Live Case Board `stale=false`.

Browser-based prompt/capture also requires an unlocked, awake macOS Aqua UI
session. The AUTOSINT UI-host keep-awake layer is scoped to that requirement:
`com.autosint.ui-host-keepawake` runs `scripts/run_autosint_ui_host_keepawake.sh`,
which execs `/usr/bin/caffeinate -dimsu` and writes only ignored logs under
`artifacts/autosint_ui_host/logs/`. It does not run prompt/capture, read
browser private state, change FileVault/Keychain/login/security settings, or
disable password policy. Check status with:

```bash
.venv/bin/python scripts/check_autosint_ui_host_status.py --once
cat artifacts/autosint_ui_host/latest/ui_host_status.md
```

`scripts/report_external_scout_24_7_proof.py` and `/external-scout/24-7` read
the latest UI-host status artifact. A RED UI-host status blocks 24/7 proof; a
GREEN or WARN non-blocking status can continue natural-cycle observation while
separate External Scout health issues are diagnosed.

## Capture Bridge

Manual status check:

```bash
PYTHONPATH=src:. .venv/bin/python -m autosint_external_scout_capture.cli --status
```

Manual dry-run capture:

```bash
PYTHONPATH=src:. .venv/bin/python -m autosint_external_scout_capture.cli --once --dry-run --prefer-files
```

Manual one-shot capture after approval:

```bash
PYTHONPATH=src:. .venv/bin/python -m autosint_external_scout_capture.cli --once --prefer-files
```

The capture bridge:

- Finds the visible `AUTOSINT External Scout Packet` ChatGPT tab by safe
  title/URL metadata.
- Prefers visible downloadable JSON/Markdown files when available.
- Falls back to visible page text extraction.

The legacy script path remains as a compatibility wrapper:

```bash
.venv/bin/python scripts/capture_chatgpt_external_scout_visible.py --status
```
- Never reads cookies, localStorage, sessionStorage, browser profile files, tokens, credential files, or `.env`.
- Writes captures through staging first.
- Promotes to inbox only when validation errors are zero.
- For multi-packet captures, may promote strict-valid packet subsets while
  quarantining invalid packet subsets with `partial_promotion=true` in the
  receipt.
- Moves fully invalid captures to quarantine.
- Writes receipts under ignored local artifacts.
- Applies recency and duplicate guards before refreshing active reports.

## Local Artifact Flow

```text
visible ChatGPT output
-> artifacts/external_scout/staging/
-> validator
-> artifacts/external_scout/inbox/ if valid
-> artifacts/external_scout/quarantine/ if invalid
-> artifacts/external_scout/latest/ report refresh
```

All of these paths are local-only and ignored by git.

## Latest Active Capture

Default External Scout review uses only the latest validated capture.

- `/external-scout` shows active latest packets only.
- `/api/v1/external-scout` returns active latest packets only.
- History is explicit through `?include_history=true` or `/api/v1/external-scout/history`.
- Older inbox captures remain archived locally but are not default promotion candidates.

## Live Case Board Rolling Retention

`/external-scout/threads` is the Live Case Board drill-down and intentionally
differs from the latest-packet inbox. The pinned operational source remains
`/external-scout/24-7`, which includes current and stale/retained thread health
from the same report chain. The thread route rebuilds topic threads from
validated packet history and applies rolling retention:

- Threads updated in the latest active capture are `current`.
- Valid threads not updated in the latest active capture remain `current`
  inside the active window, then visible as `Stale` / `stale_tracked` until
  the 72-hour tracked window expires.
- Supplemental enrichment packets update thread-current source lanes and
  timelines, but they do not define or shrink the active capture universe.
- Threads older than the tracked window move to archived/history summaries.
- Invalid or quarantined packets never update current thread state.
- HAVOC/RFI consumes thread current state first and remains review-only.
- Theater watch summaries and overflow candidate cases are displayed as
  operator context when supplied, but they do not bypass packet validation and
  do not create active threads unless a valid packet is present.

## Quality And Validation

Validation errors block inbox promotion.

Quality warnings do not necessarily block display, but they tell the operator that the packet may need review. Common non-fatal warnings include incomplete market snapshots and missing prediction-market metrics.

Pseudo-tool rows such as `finance_tool:*`, `weather_tool:*`, `not_available_from_finance_tool`, and `not_available_from_weather_tool` remain context-only and must not become proposed Evidence inserts or case links.

## Safety Boundary

External Scout capture and review must not:

- Mutate DB rows.
- Rewrite raw Evidence.
- Create case links.
- Change source configuration.
- Open OSIR gates.
- Promote commander-ready outputs.
- Add browser write controls.
- Read private browser state.

## Recommended Launchd Sequence

1. Verify Chrome visible capture works with dry-run.
2. Run one approved real capture.
3. Verify `--status` reports active packets, zero validation errors, and `stale=false`.
4. Install launchd only after separate approval.
5. Schedule local prompt submit at minute `:30`, async harvester checks while
   pending, and local capture around minute `:00`.
6. Keep launchd logs under ignored local artifacts/logs.
