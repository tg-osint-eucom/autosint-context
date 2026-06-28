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

Target production upstream:

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
conversation instead of the Packet chat, configure capture by exact
conversation id in ignored `artifacts/external_scout/capture_target.json`.
Keep local fallback prompt submission pointed at the Packet chat through
ignored `artifacts/external_scout/prompt_trigger_target.json`.

Current proven fallback timing:

```text
Prompt trigger every hour at :50.
Capture every hour at :08.
```

The local prompt trigger posts the strict Daily Scout prompt to the visible
Packet chat and waits for `packet_ready_for_capture=true`. It is fallback,
not the desired primary path. Capture then validates and promotes the latest
strict packet, or safely skips when the visible packet is already in the inbox.

Do not mark Scheduled Tasks production-ready until two natural Scheduled Task
output cycles have generated fresh strict packets in the exact configured
Scheduled Task output conversation, capture has promoted or safely skipped
equivalent strict packets with `validation_error_count=0`, Live Board has
stayed `stale=false`, and eval has no current-runtime hard-fails.

If the existing Scheduled Task cannot be safely resumed or edited, stop and
request approval before creating or replacing tasks. Do not create duplicate
tasks by default and do not create automatic per-case chats.

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
are consistently valid.

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

`/external-scout/threads` is the primary case board and intentionally differs
from the latest-packet inbox. It rebuilds topic threads from validated packet
history and applies rolling retention:

- Threads updated in the latest active capture are `current`.
- Valid threads not updated in the latest active capture remain visible as
  `Stale` / `stale_tracked` for 72 hours.
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
5. Schedule local capture around minute `:08`.
6. Keep launchd logs under ignored local artifacts/logs.
