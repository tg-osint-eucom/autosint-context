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
|   |-- source_gap_closure_notes for exact read-only source_area / lane checks
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
| Social OSINT / Public Reaction | ChatGPT External Scout | Public t.me URL checks; optional X/API or public-social adapters | Yes |
| Traffic / Movement | ChatGPT External Scout | PortWatch, Global Fishing Watch, OpenSky OAuth2/public REST, AIS, or public movement adapters | No |
| Satellite / Geospatial | ChatGPT External Scout | NASA FIRMS area CSV with `NASA_FIRMS_MAP_KEY`, Copernicus, Sentinel, or provider adapters | No |
| Weather / Environment | ChatGPT External Scout | Public weather/environment adapters | Context only |
| Prediction Markets | ChatGPT External Scout | Polymarket, Kalshi, Manifold read-only adapters | Yes |
| Markets / Finance / Stocks / Crypto | ChatGPT External Scout | Finance/enrichment adapters | Yes |
| Public Comments / Reaction | ChatGPT External Scout | Optional public comment adapters | Yes |

## Status Colors And Provider Decisions

The pinned `/external-scout/24-7` page and
`/api/v1/external-scout/24-7-proof` use one operator vocabulary for provider
state. These colors describe current operational risk; they do not authorize
Evidence import, source-config mutation, OSIR release, apply/import, or
commander-ready promotion.

| Color | Meaning |
|---|---|
| `GREEN` | A public API works, a configured read-only adapter works, or the lane is healthy with no current active blocker. Examples: Polymarket public Gamma API HTTP 200, Manifold public GET API HTTP 200, Kalshi env-gated adapter configured, Global Fishing Watch configured, OpenSky configured, FMP configured. |
| `AMBER` | Candidate found/not imported, retained or stale follow-up, blocked source URL with public alternatives, optional future provider, or non-blocking warning. Example: a social source URL is visible but no deterministic importer has been wired for that case lane. |
| `RED` | Current active blocker: stale or zero-active board, required lane missing from a current active thread, configured adapter failing when needed, credential required for a current active blocker, wrong chat, prompt not ready, or capture validation blocking current board. |

Provider rows carry these scope and decision fields:

- `credential_policy`: `public_first`, `public_api`, `configured_api`,
  `optional_later`, `paid_or_restricted`, or `not_needed_now`.
- `provider_decision`: `not_blocking`, `optional_later`,
  `retained_stale_followup`, or `current_active_blocker`.
- `provider_tier`: `public_first`, `public_api`, `configured_api`,
  `optional_later`, or `paid_or_restricted`.
- `blocker_scope`: `current_active`, `retained_stale`,
  `architecture_reference`, or `mixed`.
- `current_key_need`: `not_needed_now`, `configured_api`, `optional_later`, or
  `current_active_blocker`.
- `adapter_status`, `last_smoke_status`, and `last_http_status_summary`: safe
  proof summaries only; no credential values.

Optional future providers are architecture references, not current blockers,
unless a current active thread requires that lane and no public/configured path
can satisfy the check.

## Current Provider Truth Table

This table is the current source/provider decision contract. Credential rows
show presence/status only and never values.

| Provider / lane | Decision | Current state |
|---|---|---|
| Polymarket | `public_api` / `not_blocking` | Public Gamma API adapter present at `gamma-api.polymarket.com`; key not required; browser page blocking does not make the adapter blocked. |
| Manifold | `public_api` / `not_blocking` | Public GET API present at `api.manifold.markets`; key not required. |
| Kalshi | `configured_api` / `not_blocking` when env names are complete | Env-gated read-only signed adapter; credential presence/status only; no browser session or logged-in tab used for ingest. |
| Global Fishing Watch | `configured_api` / `not_blocking` | Traffic/movement adapter configured; token presence/status only; smoke OK. |
| OpenSky | `configured_api` / `not_blocking` | Aviation movement adapter configured; OAuth2 token path works; `states/all` smoke returned 200. |
| Financial Modeling Prep | `configured_api` / `not_blocking` | Finance quote adapter configured; AAPL profile, SPY quote, and search-symbol smoke returned 200. |
| Telegram public pages | `public_first` / `not_blocking` | Configured public `t.me` pages returned HTTP 200. |
| Telegram approved Telethon public-channel reads | `configured_api` / `not_blocking` | `TELEGRAM_API_ID`, `TELEGRAM_API_HASH`, approved channel names, and the ignored local Telethon session are present; no browser cookies, logged-in tabs, localStorage/sessionStorage, Chrome profile files, or private browser state are used. |
| NASA FIRMS | `optional_later` | Unresolved/not tested unless `NASA_FIRMS_MAP_KEY` is present and smoke passes. |

Optional future providers are not current blockers: licensed Reuters/news,
X/Twitter API, Reddit API, arbitrary Telegram scraping, translation/search API,
paid AIS/Kpler/MarineTraffic/Spire, paid freight/Baltic/Kpler/Clarksons,
Polygon/Massive, and paid satellite/Planet/Maxar/SAR.

## Source URL Status Versus Adapter Health

Source URL status and adapter health are separate. A source URL can be blocked,
paywalled, rate-limited, stale, or candidate-only while the provider adapter is
healthy.

Examples:

- A Kalshi web page can be blocked or login-required in a browser while the
  env-gated Kalshi read-only API remains configured and non-blocking.
- A Polymarket URL can be candidate-not-imported while the public Gamma API
  smoke remains GREEN.
- A public news URL can be paywalled without requiring a licensed news provider
  when public official, AP/BBC/Al Jazeera/regional/trade alternatives exist.
- Retained or stale thread source issues stay visible as follow-up memory but
  do not become current active blockers.

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
trigger in Scout Findings submit-only mode, async harvester, and `:00` capture
loop.

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
- Manifold / other prediction markets: public GET adapter first; no API key,
  login, browser session, or write endpoint is required for AUTOSINT
  cue-only market search/read checks.
- X/Twitter and social OSINT: ChatGPT public check first. Public Telegram
  `t.me` pages may be checked through plain public URL reads; approved Telegram
  Telethon public-channel reads may be used when the ignored runtime env and
  local session file are present. Telegram Telethon/session collection is an
  approved local setup and must not use private browser state.
- Finance/stocks: public checks first; provider key later if quote reliability
  demands it. Financial Modeling Prep stable API may be used through ignored
  runtime env as `FMP_API_KEY` for read-only market/finance context.
- Shipping/AIS/freight: public AIS/PortWatch and Global Fishing Watch first;
  paid provider later if maritime cases become central.
- OpenSky/ADS-B: public REST works anonymously with rate limits; approved
  OAuth2 client credentials may be loaded through ignored runtime env as
  `OPENSKY_CLIENT_ID` and `OPENSKY_CLIENT_SECRET`.
- Satellite/geospatial: NASA FIRMS/Copernicus/Sentinel first. NASA FIRMS area
  CSV requires a local `NASA_FIRMS_MAP_KEY`; paid imagery later only for
  approved high-value cases.
- News/paywall: public access only unless a licensed provider is explicitly
  approved.

## PAI Public-First Source Pack

The PAI source pack is a public-first architecture/reference list. It expands
the discovery itinerary without creating API blockers or a source registry. Each
source is classified in `config/autosint_sensor_architecture.yml` with
`source_family`, `provider_tier`, `provider_decision`, `primary_checker`,
`fallback_checker`, `cue_only`, `proof_capable`, `key_required`,
`current_key_need`, and access notes.

The current pack includes defense/security media, regional and international
public media, think tanks, military journals, public movement/geospatial
sources, and public archives such as Real Clear Defense, Defense News, Defense
One, BBC, Al Jazeera, War on the Rocks, Foreign Policy, Bellingcat, LiveUAMap,
ADS-B Exchange, NGA Map of the World, Wayback Machine, RAND, ISW, IISS, CSIS,
RUSI, Naval War College Review, Army Parameters, and related public-first
sources. Paywalled, restricted, or licensed access is marked as optional/future
unless it becomes an approved current active need.

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
