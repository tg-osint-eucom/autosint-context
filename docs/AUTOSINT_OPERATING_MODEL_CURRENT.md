# AUTOSINT Operating Model Current

AUTOSINT is a local-first operational intelligence review stack. ChatGPT External Scout collects public candidate packets, while AUTOSINT validates, quality-checks, normalizes, deduplicates, previews source candidates, maps topics into theater/workspaces, and produces HAVOC/RFI package previews.

ChatGPT packets are candidate input only. Nothing becomes Evidence, no case link is created, no source configuration is changed, and no OSIR or commander-ready gate opens without a future explicit controlled approval workflow. Market, social OSINT, prediction-market, crypto, and public-comment material remains cue-only context.

Repo-level Codex execution rules, including the active autopush gate and
Codex context/memory source-of-truth rule, are maintained in `AGENTS.md`.
Codex memories are helper recall only; durable project rules must be tracked in
`AGENTS.md` or repo docs, and current thread context is temporary.

ChatGPT Project operating rules are maintained in
`docs/AUTOSINT_CHATGPT_PROJECT_OPERATING_MODEL.md`. The key rule is that
AUTOSINT Live Case Board threads are durable case memory, while ChatGPT Project
chats are controlled workspaces only.

For substantial multi-step work, use `/goal` so objectives, validation gates,
and stop conditions are explicit. After meaningful commits that change
workflow, architecture, validation status, or operator behavior, refresh the
public `autosint-context` mirror.

## Primary Operator Workflow

The current primary workflow is:

```text
Mission Control -> External Scout 24/7 Control Page -> Live Case Board drill-down -> TSOC/HAVOC -> HAVOC/RFI -> future controlled approval
```

Primary browser routes:

- `/mission-control`
- `/external-scout/24-7`
- `/external-scout/threads`
- `/tsoc-havoc`
- `/havoc-rfi/SOCCENT`

Supporting and audit routes:

- `/external-scout`
- `/api/v1/external-scout/24-7-proof`
- `/case-genesis`
- `/canonical-cases`
- `/api/v1/cases/{case_id}/osir`
- `/api/v1/cases/{case_id}/evidence-passport`
- `/api/v1/cases/{case_id}/audit-bundle`
- `/api/v1/pirs`
- `/api/v1/pir-observations`
- `/api/v1/overwatch`
- `/api/v1/agent-feed`
- `/api/v1/agent-threads/{thread_id}`
- `/api/v1/agent-roster`

Removed legacy browser routes:

- `/dagrbook`
- `/moltbook`
- `/control-plane`

These legacy routes should remain removed from primary navigation unless a future frontend-thread rebuild explicitly restores them.

## External Scout Pipeline

The current proven External Scout path is:

```text
ChatGPT Project / Packet-chat prompt trigger in Scout Findings mode
-> pending generation receipt if Pro Extended starts but is not ready
-> async Scout Findings harvester checks the same Packet turn
-> visible Scout Findings JSON or downloadable Scout Findings attachment
-> deterministic AUTOSINT normalizer
-> strict packet staging
-> validation
-> quarantine if invalid
-> active inbox if valid and newer than latest inbox
-> latest active capture only
-> /external-scout
-> /havoc-rfi
```

As of 2026-07-02, Pro Extended is treated as a source-discovery/findings
generator rather than the strict-packet author. The prompt-trigger wrapper
defaults to `--scout-findings-mode`; it accepts current Scout Findings JSON or
the visible `autosint_scout_findings_YYYYMMDDTHHMMSSZ.json` attachment,
normalizes with
`scripts/normalize_external_scout_findings_to_packets.py`, and promotes only a
validator-clean packet set with `commander_ready=false` and
`mutation_performed=false`. Direct ChatGPT strict packets remain candidate
fallback material, not the preferred Pro Extended machine-output contract.

If Pro Extended starts answering but no Scout Findings `generated_at` is ready
immediately after verified submit, the prompt-trigger records
`scout_findings_pending` under ignored pending-generation artifacts and exits
instead of waiting on the same Pro Extended renderer. It does not submit a
duplicate prompt or stop/reload the existing turn. The async harvester
(`scripts/harvest_external_scout_findings.py`) re-checks that exact pending
Packet request, extracts a visible Scout Findings JSON/attachment when
available, runs the deterministic normalizer, and promotes only when
normalization validates cleanly and the output is newer than inbox. Stale or
mismatched findings remain recorded as harvest receipts and do not refresh
active recovery.

ChatGPT Scheduled Tasks remain an active but unverified upstream candidate. On
2026-06-28, the existing Scheduled Task was updated and resumed, but its proof
run did not expose a capturable output conversation or advance the Packet chat
before `:08`; the local Packet-chat trigger restored the board with receipt
`20260628T192327Z_prompt_trigger_receipt.json` and capture receipt
`20260628T193810Z_capture_receipt.json`. A later outside-project task-result
conversation was visible, but dry-run validation found twelve
`source_relationships` bucket type errors; the prompt was tightened and the
task was updated, while Packet fallback again promoted five valid packets with capture receipt
`20260628T200809Z_capture_receipt.json`. Do not treat Scheduled Tasks as
production-primary until two natural output -> capture cycles pass through the
dedicated scheduled-task probe or capture path. The same proof found a
strict-valid Scheduled Task result generated_at `2026-06-28T20:05:53Z`, but it
was not promoted because the Packet fallback had already produced a newer inbox
packet and because outside-project result chats are not production targets.
This means proof must avoid upstream competition and must stay inside the
AUTOSINT External Scout Project; otherwise Packet fallback remains the correct
production source. The current live Scheduled Task state is paused, which is
intentional containment until ChatGPT can produce output in the Project Packet
chat or another Project-scoped output conversation. After the outside-project
result chat was deleted, the visible task editor was checked read-only and
showed no output chat, Project, or conversation target selector, so there is no
safe UI control currently available to bind the task to the Project Packet chat.

Operational rules:

- Valid captures go through staging and validation before inbox promotion.
- Invalid or schema-drifted captures go to quarantine and do not refresh active reports.
- `/external-scout` defaults to the latest validated capture only.
- History remains available through explicit history mode and ignored local artifacts.
- Capture receipts, logs, inbox files, staging files, quarantine files, and latest generated reports are local-only and ignored.
- The stale rule is currently 90 minutes.
- ChatGPT scheduled output timing has drifted and may remain visible as
  `Выполняется` past the local capture window; prove with the scheduled-task
  probe before changing production targets.
- Do not resume a Scheduled Task that only creates outside-project
  `chatgpt.com/c/...` result chats.
- The local Packet-chat loop is not considered 24/7-proven from a single green
  run. Use `scripts/report_external_scout_24_7_proof.py` and require three
  consecutive natural async prompt -> harvester proof cycles before declaring
  24/7 readiness.
- Operators should keep `/external-scout/24-7` as the single pinned External
  Scout operator tab. It reads the same canonical proof report as
  `/api/v1/external-scout/24-7-proof` and includes Live Board freshness,
  current/stale case health, source gaps, enrichment gates, logs, and drill-down
  links. `/external-scout/threads`, `/external-scout`, and HAVOC/RFI are
  read-only drill-downs, not separate control surfaces.
- Planned async local AUTOSINT timing is prompt at minute `:00` and exact
  Packet v2 prewarm/harvest at minute `:28`. Direct capture remains available
  as manual diagnostic/emergency tooling only, not as a scheduled production
  fallback.
- The launchd template may exist locally, but installing/loading launchd is a separate approval.

## HAVOC/RFI Packet-Driven Behavior

HAVOC/RFI packages select the best validated External Scout packet by workspace. SOCCENT selects a Hormuz / Strait of Hormuz / Iran Gulf maritime-risk packet when present.

The package leads with External Scout operator fields:

- BLUF
- What Changed
- So What
- Source Relationships
- Traffic / Logistics
- Market Reaction
- Prediction-Market Reaction
- Geospatial Context
- Weather Context
- Decision
- Collection Plan
- System Status

Canonical cases, Case Genesis, TSOC/HAVOC, source coverage, and provenance remain available as Audit Details or supporting material. If no suitable External Scout packet exists, HAVOC/RFI falls back to committed baseline TSOC/canonical/case-genesis material and should clearly state that no validated External Scout packet was selected.

## External Scout Live Case Board

`/external-scout/threads` is the External Scout Live Case Board drill-down. The
pinned operational view is `/external-scout/24-7`, which reads the same
AUTOSINT proof/report chain and shows the Live Board state, current/stale case
source health, and source-gap queues in one place. `/external-scout` remains
the latest active packet inbox and support view.

The Live Case Board:

- Groups packets by stable topic.
- Appends new captures to existing topic threads.
- Shows what changed since the previous capture.
- Maintains per-topic timelines and previous packets.
- Marks threads as New, Updated, Stale, Escalating, or Needs Review.
- Keeps latest-capture topics current, keeps recently unupdated topics current
  inside the active window, retains older unupdated topics as stale tracked
  threads until the 72-hour tracked window expires, and moves older threads to
  audit/history.
- Treats supplemental enrichment packets as thread-lane overlays; they can
  improve current thread source status, but they do not define or shrink the
  active capture universe.
- Lets HAVOC/RFI consume current thread state before raw-packet fallback.
- Shows theater watch summaries when supplied by strict output:
  SOCCENT, SOCEUR, SOCPAC, SOCAFRICA, SOCSOUTH, SOCKOR, and SOCOMD must be
  explicitly checked, no-case, or omitted/overflow with a reason.
- Keeps omitted or overflow candidate cases visible as review context without
  letting them replace active validated thread state.

ChatGPT Project chats must not replace this board as case memory. The scheduled
Daily Scout chat is machine-output only, `AUTOSINT System Control` is the
human/admin workspace, and optional `CASE - <topic>` chats are human-created
deep dives only for important cases.

Initial thread topics include:

- Hormuz / Strait of Hormuz / Iran Gulf maritime risk
- Lebanon / Israel / Hezbollah ceasefire
- Ukraine refinery and energy strikes
- Taiwan grey-zone activity
- Scarborough Shoal
- Niamey airport

## Global Sensor Coverage

External Scout packets must not silently omit required source/sensor lanes.
The policy is tracked in `docs/AUTOSINT_GLOBAL_SENSOR_COVERAGE_POLICY.md` and
`config/autosint_sensor_coverage_policy.yml`.

Required packet output includes explicit rows for case coverage,
market/finance, prediction markets, multilingual/regional context, traffic and
movement, geospatial/satellite, weather/environment, social/public reaction,
and cue-only lanes. Each row must use an explicit state such as checked and
found, checked and not found, candidate found but not imported, not checked,
stale, or blocked/login required.

Theater watch behavior is tracked in `docs/AUTOSINT_THEATER_WATCH_POLICY.md`
and `config/autosint_theater_watch_policy.yml`. ChatGPT output may emit up to
five active packets, but the theater watch summary must still report what was
checked across all major theaters and list omitted or overflow candidates when
the credible case set exceeds the active packet limit.

## Agents, PIR, And Legacy Surfaces

PIR Hunter is active as a backend/API/MCP support capability, not a primary browser workflow. It should become a priority-question / exception layer connected to External Scout and TSOC/HAVOC.

Operator Hub and Operator Scheduler are supporting source-gap and discovery systems. They must remain isolated from `core.worker` unless explicitly approved.

Agent Exchange is audit/provenance and case-assist infrastructure. Agent write tools must remain gated and disabled unless a future controlled approval path explicitly enables them.

MOLTBook/DAGRBook browser routes have been removed from the current primary browser path. DAGRBook assets and helper code remain preserved for future frontend-thread work.

## Source Policy

Serious-case priority source families:

- Official / Advisory
- Public News
- Traffic / Movement
- Satellite / Geospatial, where relevant

Cue-only source families:

- Social OSINT
- Telegram / X / Reddit
- Markets / Finance
- Prediction Markets
- Crypto / on-chain
- Public comments

Conditional source roles:

- Etherscan: crypto/on-chain cue only.
- ReliefWeb: humanitarian/logistics context only.
- NASA FIRMS: geospatial/thermal cue only; API checks require local `NASA_FIRMS_MAP_KEY`.
- Sentinel/Copernicus: geospatial context.
- AIS/GFW/PortWatch: traffic/movement; Global Fishing Watch token goes through ignored runtime env.
- OpenSky/ADS-B: aviation movement; OAuth2 client credentials go through ignored runtime env when configured, with anonymous public REST as bounded fallback.
- Financial Modeling Prep: market/finance quote and profile context; `FMP_API_KEY` goes through ignored runtime env and remains cue-only.
- Polymarket/Kalshi: probability/sentiment cue only.

## What Not To Delete Yet

Do not remove these until replacements are designed and validated:

- Canonical cases.
- Case Genesis.
- Evidence passports.
- OSIR gates and OSIR policy surfaces.
- Source coverage and source discovery scripts.
- Source registries and sensor registry files.
- DAGRBook assets/helpers.
- Agent harness.
- Operator Scheduler.
- PIR Hunter / Overwatch APIs.

## Likely Future Cleanup Candidates

Likely deprecate or delete later after replacement:

- Old debug browser routes already removed from entrypoints.
- Low-level pages not in the primary workflow.
- Duplicate source-discovery UI if External Scout fully replaces it.
- Stale report-only artifacts after migration into Source Library/audit.
- Duplicated HAVOC wording builders if packet-driven mode remains stable.
- Legacy Moltbook wording after Agent Exchange terminology fully replaces it.

## Safety Boundary

Current safety boundary:

- No DB mutation from review pages.
- No raw Evidence mutation.
- No case-link mutation.
- No source config mutation.
- No OSIR bypass.
- No apply/import path.
- No commander-ready promotion.
- ChatGPT packets are candidate input only.
- Market, social OSINT, prediction-market, crypto, and public-comment data are cue-only.

## One-Page Mental Model

```text
ChatGPT Scout finds public signals.
AUTOSINT validates packets.
External Scout shows candidate packets.
TSOC/HAVOC groups by theater.
HAVOC/RFI writes operator preview.
OSIR blocks commander-ready.
Future approval imports selected source URLs.
```
