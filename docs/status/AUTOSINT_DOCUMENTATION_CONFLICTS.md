# AUTOSINT Documentation Conflicts

- Status: Current audit register
- Authority: Supporting conflict register; higher-authority sources decide each row
- Version: 2.1
- Owner: AUTOSINT Documentation
- Last reviewed: 2026-07-19
- Runtime truth: No
- Supersedes: Preliminary 41-file conflict counts and open owner decisions
- Superseded by: None
- Related: [System Contract](AUTOSINT_SYSTEM_CONTRACT_CURRENT.md), [Documentation Authority](AUTOSINT_DOCUMENTATION_AUTHORITY.md), [Documentation Index](AUTOSINT_DOCUMENTATION_INDEX.md)

## Final Disposition

| ID | Topic | Confirmed conflict | Deciding authority | Final disposition |
|---|---|---|---|---|
| `DOC-C001` | Producer mode | Highest-authority wording did not distinguish Scout Findings producer output from normalized strict packets. | `AGENTS.md` and `config/autosint_system_contract.yml` | `RESOLVED_BY_SYSTEM_CONTRACT`: Scout Findings default; direct strict packets fallback/replay only. |
| `DOC-C002` | Transport | Current drafts described inline and attachment as competing primary transports. | System contract, prompt, harvester, and focused tests | `RESOLVED_BY_SYSTEM_CONTRACT`: inline primary, attachment fallback, never both full payloads. |
| `DOC-C003` | Case count | Current docs mixed a five-case default with a lower bounded mode. | System contract | `RESOLVED_BY_SYSTEM_CONTRACT`: natural 1-3, absolute maximum 5, bounded recovery exactly 1. |
| `DOC-C004` | Schedule and direct capture | Historical direct-capture and Scheduled Task wording appeared beside the current loop. | Current runtime code and runbook | `RESOLVED_BY_CURRENT_RUNBOOK`: local scheduled prompt then async harvester; direct capture manual-only. |
| `DOC-C005` | Sensor requirements | The trace called Manifold and insurance/freight future while current policy required them. | System contract, validator, normalizer, preservation tests | `RESOLVED_BY_IMPLEMENTATION`: both are required first-class rows. |
| `DOC-C006` | Semantic preservation | Schema-clean packets were described as sufficient despite possible dropped semantic fields. | Preservation contract and three promotion-gate counters | `RESOLVED_BY_IMPLEMENTATION`: structural, semantic, and preservation errors must all be zero. |
| `DOC-C007` | Package summary | A preliminary package reported zero conflicts/owner decisions while its matrices contained them. | Deterministic documentation consistency builder | `RESOLVED_BY_DERIVATION`: all counts are calculated from matrix and manifest rows. |
| `DOC-C008` | Workstream history | Current projection and dated runtime narratives occupied one current status document. | `config/autosint_workstreams.yml` plus generated projection | `RESOLVED_BY_PROJECTION`: current status table is generated; runtime history is not current proof. |
| `DOC-C009` | Product routes | Current material used multiple preview names and route families. | System contract and registered API routes | `RESOLVED_BY_RFI_MIGRATION`: `/rfi` and `/rfi/{workspace}` only. |
| `DOC-C010` | Model policy and attribution | Required Project selection could be mistaken for machine-verified cycle/API identity. | System contract and official OpenAI product docs | `MANUAL_VERIFICATION_REMAINS`: selection is operator-confirmed; account verification is not performed; cycle attribution requires a receipt; API id is not inferred. |
| `DOC-C011` | Historical Threads precedence | Superseded design wording did not explain whether the status order was worst-state rollup. | Current thread rollup code; archival note | `HISTORICAL_VALID_AT_TIMESTAMP`: the historical order is explicitly labelled worst-state and non-current. |
| `DOC-C012` | Graph retrieval | Proposed architecture language could be read as a current GraphRAG implementation. | Current code/config plus proposal headers | `PROPOSED_CORRECTLY_LABELLED`: canonical event/provenance contracts first; GraphRAG remains `EVALUATE_LATER`. |
| `DOC-C013` | Current state versus V2.1 target | Accepted architecture documents could be read as current production or pilot acceptance. | `AUTOSINT_CURRENT_STATE.md`, code/config/tests, current receipts, and acceptance gates | `RESOLVED_BY_TRUTH_SCOPE`: current repository implementation, live runtime, accepted target, and pilot acceptance remain separate snapshots. `TARGET_NOT_ACCEPTED` remains explicit. |
| `DOC-C014` | PIR Hunter | Earlier documentation classified PIR as backend/planned while dedicated routes and a default replay service are now registered. | Current PIR code/routes/tests plus current-state classification | `RESOLVED_BY_CURRENT_IMPLEMENTATION`: `REGISTERED_READ_ONLY_REPLAY`; no current PostgreSQL PIR data, production automation, or Evidence/case/source authority is claimed. |
| `DOC-C015` | Agent collaboration | Roster/storage language and deterministic demo output could be mistaken for live autonomous agent communication. | Typed runtime/event-store code, registered GET routes, fixtures, and current DB/runtime evidence | `RESOLVED_BY_TRANSPORT_EVIDENCE`: bounded typed replay and a labelled demo exist; `DETERMINISTIC_REPLAY_FIXTURE` is not production delivery or current communication proof. |
| `DOC-C016` | PostgreSQL foundation | Tracked Compose, manager, and Alembic files could be mistaken for a running/migrated service. | PostgreSQL manager/status receipts and migration/backup gates | `RESOLVED_BY_RUNTIME_GATE`: `TRACKED_OFFLINE_IMPLEMENTATION`; live mutation remains stopped by `EXISTING_DATABASE_REQUIRES_OPERATOR_DECISION`. |
| `DOC-C017` | MCP canonicalization | Tracked MCP code and inventories could be confused with the currently loaded external binding. | Current bounded rebind/handshake receipt plus canonical server inventories | `RESOLVED_BY_CURRENT_RECEIPT`: the recorded run is `MCP_CANONICAL_READONLY_PROVEN`, with write gates off and no write call; future sessions must revalidate binding and gates. |
| `DOC-C018` | Operator UI V2 | Same-server preview routes could be described as the production operator replacement before browser QA/UAT. | Registered routes/config/tests, browser QA receipts, and acceptance gates | `RESOLVED_BY_DEFAULT_OFF_PREVIEW`: `DEFAULT_OFF_LOCAL_PREVIEW`; the current External Scout operator routes remain primary until explicit acceptance. |
| `DOC-C019` | Safe archive and mirror paths | Archived source paths and the earlier hard-coded mirror list could leave stale references or drop a previously mirrored historical file. | Archive manifest/reference tests plus documentation registry and mirror publisher | `RESOLVED_BY_REGISTRY_AND_MOVE_PAIRS`: three move pairs preserve history, the archived capture boundary retains mirror eligibility, and no `DEAD_CONFIRMED` deletion or mirror publication is implied. |

## Remaining Manual Boundary

No private account or Project setting is inspected. The exact saved Project
Instructions remain `NOT_VERIFIED_OPERATOR_SETTING` until the operator provides
a plain-text copy and the deterministic comparison script passes. This is a
manual verification boundary, not an unresolved producer/transport decision.

## Counting Rule

This register is evidence/navigation, not a handwritten summary source. Final
conflict, stale, unsupported, operator-decision, finding, and verdict counts are
derived from machine-readable matrices by the documentation consistency
builder. Material claims still require direct code/config/test/receipt evidence.
