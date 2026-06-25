# AUTOSINT Operating Model Current

AUTOSINT is a local-first operational intelligence review stack. ChatGPT External Scout collects public candidate packets, while AUTOSINT validates, quality-checks, normalizes, deduplicates, previews source candidates, maps topics into theater/workspaces, and produces HAVOC/RFI package previews.

ChatGPT packets are candidate input only. Nothing becomes Evidence, no case link is created, no source configuration is changed, and no OSIR or commander-ready gate opens without a future explicit controlled approval workflow. Market, social OSINT, prediction-market, crypto, and public-comment material remains cue-only context.

Repo-level Codex execution rules, including the active autopush gate, are maintained in `AGENTS.md`.

ChatGPT Project operating rules are maintained in
`docs/AUTOSINT_CHATGPT_PROJECT_OPERATING_MODEL.md`. The key rule is that
AUTOSINT Live Case Board threads are durable case memory, while ChatGPT Project
chats are controlled workspaces only.

## Primary Operator Workflow

The current primary workflow is:

```text
Mission Control -> External Scout -> TSOC/HAVOC -> HAVOC/RFI -> future controlled approval
```

Primary browser routes:

- `/mission-control`
- `/external-scout`
- `/tsoc-havoc`
- `/havoc-rfi/SOCCENT`

Supporting and audit routes:

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

The External Scout path is:

```text
ChatGPT Project / scheduled task
-> visible-browser capture bridge
-> staging
-> validation
-> quarantine if invalid
-> active inbox if valid
-> latest active capture only
-> /external-scout
-> /havoc-rfi
```

Operational rules:

- Valid captures go through staging and validation before inbox promotion.
- Invalid or schema-drifted captures go to quarantine and do not refresh active reports.
- `/external-scout` defaults to the latest validated capture only.
- History remains available through explicit history mode and ignored local artifacts.
- Capture receipts, logs, inbox files, staging files, quarantine files, and latest generated reports are local-only and ignored.
- The stale rule is currently 90 minutes.
- ChatGPT scheduled output has been observed around minute `:03` of each hour.
- Planned local AUTOSINT capture timing is minute `:08` of each hour.
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

`/external-scout/threads` is the primary External Scout Live Case Board. It rebuilds durable read-only topic threads from validated External Scout history, while `/external-scout` remains the latest active packet inbox and support view.

The Live Case Board:

- Groups packets by stable topic.
- Appends new captures to existing topic threads.
- Shows what changed since the previous capture.
- Maintains per-topic timelines and previous packets.
- Marks threads as New, Updated, Stale, Escalating, or Needs Review.
- Keeps latest-capture topics current, retains recently unupdated topics as
  stale tracked threads for 72 hours, and moves older threads to audit/history.
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
- NASA FIRMS: geospatial/thermal cue only.
- Sentinel/Copernicus: geospatial context.
- AIS/GFW/PortWatch: traffic/movement.
- OpenSky/ADS-B: aviation movement.
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
