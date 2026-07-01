# AUTOSINT Sensor Architecture v1

AUTOSINT Sensor Architecture v1 is the durable contract for how External Scout
discovers public signals, how AUTOSINT validates them, and how the operator sees
the loop on the pinned `/external-scout/24-7` page.

This document is read-only architecture. It does not authorize DB writes, raw
Evidence writes, case links, source-config mutation, OSIR release, apply/import,
commander-ready promotion, launchd changes, credential collection, private
browser-state access, login bypass, CAPTCHA bypass, or paywall bypass.

## Core Rule

```text
ChatGPT External Scout discovers broadly.
AUTOSINT validates strictly.
Adapters verify deterministically.
Live Board remembers cases.
Health monitor watches the loop.
HAVOC/RFI previews only.
Nothing becomes Evidence, OSIR, case-linked, applied/imported, or commander-ready
without a future explicit approval gate.
```

No required source or sensor lane may be silently omitted. Each lane must report
one explicit status:

- `Checked and found`
- `Checked and not found`
- `Candidate found, not imported`
- `Not checked`
- `Stale`
- `Blocked / login required`

Markets, prediction markets, crypto, social OSINT, and public comments are
cue-only. They never prove attribution, causality, intent, closure, reopening,
insider activity, OSIR release, or commander-ready intelligence.

## Pipeline Map

```text
WORLD / PUBLIC SIGNALS
|
|-- A. ChatGPT External Scout upstream
|   |-- theater watch for SOCCENT, SOCEUR, SOCPAC, SOCAFRICA, SOCSOUTH, SOCKOR, SOCOMD
|   |-- source/sensor itinerary per serious case
|   |-- up to five candidate_packets
|   |-- theater_watch_summary for all required theaters
|   |-- overflow_candidate_cases when more than five credible cases exist
|   `-- strict JSON first, concise Markdown second
|
|-- B. AUTOSINT Capture Layer
|   |-- Packet chat / scheduled task output / future API output
|   |-- request-id readiness checks
|   |-- scroll-to-latest and Copy Response fallback when visible-browser extraction is ambiguous
|   |-- dry-run validation
|   `-- real capture only when validation path is safe
|
|-- C. AUTOSINT Validator / Gate
|   |-- schema validation
|   |-- required field validation
|   |-- source/sensor lane validation
|   |-- theater_watch_summary validation
|   |-- market/prediction/finance validation
|   |-- cue-only discipline
|   |-- commander_ready=false
|   |-- mutation_performed=false
|   `-- no Evidence / no OSIR / no case-link / no apply
|
|-- D. Promotion / Quarantine
|   |-- valid packets -> inbox
|   |-- invalid packets -> quarantine
|   |-- mixed packet set -> partial promotion
|   `-- invalid packets never update active case state
|
|-- E. Thread Builder / Case Memory
|   |-- canonical topic_key
|   |-- active threads from latest capture plus still-fresh active-window memory
|   |-- stale tracked threads
|   |-- archived threads
|   |-- timeline append
|   |-- supplemental enrichment overlays that update lanes without shrinking active universe
|   |-- source_topic_keys / lineage audit
|   `-- preserve stronger current state if a later packet is weaker
|
|-- F. Post-Capture Enrichment / Adapters
|   |-- Kalshi read-only adapter
|   |-- Polymarket public checks
|   |-- Manifold / other prediction markets
|   |-- market / stocks / defense / crypto checks
|   |-- insurance / freight / rates
|   |-- candidate source URL inventory
|   |-- public URL verification
|   `-- future adapters: X API, AIS, satellite, finance provider
|
|-- G. Operator Surfaces
|   |-- /external-scout/24-7 single pinned proof / health / source-health page
|   |-- /external-scout/threads drill-down case memory
|   `-- /havoc-rfi/SOCCENT analyst-review-only preview
|
`-- H. Health / Eval / Alerts
    |-- health monitor GREEN/WARN/RED
    |-- RED alert plus codex_ready_recovery_prompt
    |-- eval dataset v1 deterministic checks
    `-- recovery playbook with safe Packet chat handling
```

## Source / Sensor Itinerary

Every serious case should account for these lanes. If a source cannot be
checked, blocked, stale, or unavailable, report that explicitly.

| Lane | Primary checker | Deterministic follow-up | Cue-only |
|---|---|---|---|
| Official / Advisory | ChatGPT External Scout | Public URL verifier / official adapters | No |
| Public News / Wires / Trade Press | ChatGPT External Scout | Public URL verifier / licensed news adapter if approved | No |
| Multilingual / Regional | ChatGPT External Scout | Optional translation/search adapters | No |
| Social OSINT / Public Reaction | ChatGPT External Scout | Optional X/API or public-social adapters | Yes |
| Traffic / Movement | ChatGPT External Scout | PortWatch, OpenSky, AIS, or public movement adapters | No |
| Satellite / Geospatial | ChatGPT External Scout | NASA FIRMS, Copernicus, Sentinel, or provider adapters | No |
| Weather / Environment | ChatGPT External Scout | Public weather/environment adapters | Context only |
| Prediction Markets | ChatGPT External Scout | Polymarket, Kalshi, Manifold read-only adapters | Yes |
| Markets / Finance / Stocks / Crypto | ChatGPT External Scout | Finance/enrichment adapters | Yes |
| Public Comments / Reaction | ChatGPT External Scout | Optional public comment adapters | Yes |

## URL Lifecycle

```text
0. Discovered
1. Classified by source/sensor lane
2. Access checked as public, blocked, paywalled, rate-limited, not fetched, or unsafe
3. Extracted safely as title, publisher, timestamp, short paraphrase, and visible facts
4. Mapped to case lane: claim, counter-claim, observed, advisory, context, or missing
5. Assigned an explicit lane status
6. Stored as candidate memory and source health on /external-scout/24-7
7. Future approved import only through a separate explicit approval path
```

Candidate source URL inventory and verification are local candidate memory only.
They do not import Evidence, create case links, mutate source config, open OSIR,
perform apply/import, change commander-ready state, use browser cookies/sessions,
read Chrome profile state, bypass login/CAPTCHA/paywalls, or print credential
values.

## Case Lifecycle

```text
0. Candidate signal
1. Strict candidate packet
2. Validation
3. Thread creation/update
4. Active
5. Continued / recurring
6. Stale tracked
7. Archived
```

Create or update a case only from a valid packet with a normalized topic,
workspace, explicit source/sensor lanes, and passing validation. Continue an
existing case when the canonical topic repeats with new source-family,
market/social/geospatial, or theater-watch changes. Stale and archived states
must stay visible as continuity and audit memory, not current active truth.

## Upstream Choices

The desired future upstream is a Project-scoped ChatGPT Scheduled Task that
emits strict packets into a known output conversation. Until that path is proven
through natural cycles, the proven upstream remains the local Packet-chat prompt
trigger and `:08` capture loop.

The current production split is:

```text
Scheduled Task = desired primary upstream after proof
Local prompt trigger = production fallback / current proven upstream
AUTOSINT capture and validator = source of truth
Live Board = durable case memory
```

## API / Key Decision Tree

Use ChatGPT External Scout first for broad public discovery. Add deterministic
adapters only when repeatability, metrics, or persistent gaps justify them.

- Polymarket: public adapter first; no key usually required.
- Kalshi: read-only API is useful for richer deterministic checks; credentials
  must use ignored runtime env helpers and never be pasted into chat or commits.
- Manifold / other prediction markets: public adapter first.
- X/Twitter and social OSINT: ChatGPT public check first; official API only if
  automatic ingest becomes necessary.
- Finance/stocks: public checks first; provider key later if quote reliability
  demands it.
- Shipping/AIS/freight: public AIS/PortWatch first; paid provider later if
  maritime cases become central.
- Satellite/geospatial: NASA FIRMS/Copernicus/Sentinel first; paid imagery later
  only for approved high-value cases.
- News/paywall: public access only unless a licensed provider is explicitly
  approved.

## Operator Surface Contract

`/external-scout/24-7` is the single pinned operator surface for this pipeline.
It should show:

- Sensor Pipeline status.
- Provider / Source Lane Matrix.
- Credential blockers with presence/status only.
- Next safe actions.
- Live Board freshness.
- Source health by case.
- Prompt/capture receipts.
- Eval and health status.

`/external-scout/threads`, HAVOC/RFI, API JSON, receipts, logs, and generated
artifacts remain drill-down verification views, not separate control surfaces.
