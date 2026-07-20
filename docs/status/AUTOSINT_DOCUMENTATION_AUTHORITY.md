# AUTOSINT Documentation Authority

- Status: Current
- Authority: Canonical documentation governance
- Version: 2.1
- Owner: AUTOSINT Documentation
- Last reviewed: 2026-07-19
- Supersedes: Implicit document precedence and ad hoc documentation allowlists
- Superseded by: None
- Runtime truth: No; current runtime claims require the applicable receipt-backed authority
- Related: [Documentation Index](AUTOSINT_DOCUMENTATION_INDEX.md), [Documentation Conflicts](AUTOSINT_DOCUMENTATION_CONFLICTS.md), [Current State](AUTOSINT_CURRENT_STATE.md), [Architecture Decisions V2.1](../architecture/AUTOSINT_ARCHITECTURE_DECISIONS_V2_1.md), [AGENTS.md](../../AGENTS.md)

## Authority Inventory

`config/autosint_documentation_authority.yml` is the machine-readable inventory
for applicable current, target, proposal, generated, and historical documents.
It owns:

- the required eight-field durable metadata contract;
- each document's authority class and truth scope;
- the bounded generated-identity exception;
- deterministic documentation index coverage;
- the sanitized context-mirror input set.

The registry is navigation and consistency authority. It does not override the
field authority inside code, config, tests, current receipts, or the repository
constitution. `AUTOSINT_CURRENT_STATE.md` separates current repository
implementation from live runtime and target state.
`AUTOSINT_ARCHITECTURE_DECISIONS_V2_1.md` records accepted target decisions
without upgrading them to runtime truth.

## Precedence

1. Product/system safety and explicit current task scope.
2. Nearest applicable `AGENTS.override.md` or `AGENTS.md`.
3. Current tracked code, config, schemas, tests, and field-authoritative docs.
4. Current receipt-backed runtime reports for live-state fields.
5. Sanitized context mirror for durable recovery context only.
6. Generated audits and historical records as evidence pointers.

When sources conflict, compare authority, commit and receipt identity, and
timestamps. Do not merge fields from different snapshots into one apparent
current state. Target architecture never silently supersedes the current
production default.

## Canonical Ownership Matrix

| Topic | Primary authority | Supporting authority | Not sufficient |
|---|---|---|---|
| Repository rules | `AGENTS.md` | Documentation authority registry | Chat summaries, memory, or target docs. |
| Current-versus-target classification | Current code/config/tests plus `AUTOSINT_CURRENT_STATE.md` | V2.1 ADRs and workstreams | Proposal status or route HTTP 200. |
| Operating model | `docs/AUTOSINT_OPERATING_MODEL_CURRENT.md` | Primary workflow | Historical reports. |
| Operator routes | `docs/AUTOSINT_PRIMARY_WORKFLOW.md` plus registered routes | API and rendered-route tests | README alone. |
| External Scout runtime | Current code, receipts, proof and health reports | External Scout Runbook | Screenshot, old receipt, or retained board. |
| Scout Findings output | Current prompt contract, harvester, normalizer, runbook | Project operating model | Strict-packet fixture alone. |
| Pending lifecycle | Current pending/harvester code and receipts | Runbook | Visible Stop control alone. |
| Proof and health | Canonical proof/health reporters | Runbook | HTTP 200 or a single success. |
| Sensor architecture | Config, capability registry, normalizer, validator | Sensor architecture and policies | Row presence alone. |
| 13 categories | Global sensor policy and tracked config | Sensor architecture | 19-lane count. |
| 19 lanes | `config/autosint_sensor_architecture.yml` and capability registry | Sensor architecture | Placeholder rows. |
| Theater watch | Theater Watch Policy and compatible typed evidence | Sensor config | Candidate URL or old packet. |
| Markets/prediction | Market, Prediction, Finance Policy | Validator | Cue-only metric as proof. |
| Threads and Live Board | Current thread code/routes/tests and Primary Workflow | Acceptance trace | Chat workspace or retained data. |
| PostgreSQL | Alembic chain, manager, DB runbooks, current service receipts | Production Architecture V2.1 | Tracked migration files as live migration proof. |
| PIR Hunter | Current PIR code/routes/tests and current-state classification | PIR architecture target | Module existence or replay fixture as current DB data. |
| Agent Runtime | Manager, typed contracts, event store, routes, tests | Agent Runtime target | Roster, sender ID, or fixture alone. |
| Agent Collaboration Room | Typed event projection, registered read route, tests | Collaboration Room target | Static feed or demo as production delivery. |
| ScoutGenerationService | Current contracts/providers/tests | Generation Service architecture | Provider adapter existence as production enablement. |
| MCP | Canonical server code/inventories plus current rebind receipt | MCP Boundary V1 | Prior binding or tool listing alone. |
| Operator UI V2 | Registered same-server routes/config/tests plus browser QA | UI target and information hierarchy | Default-off implementation as production acceptance. |
| RFI | Current code/routes/tests | Operating model and primary workflow | Preview as commander-ready. |
| Evidence / OSIR | Current DB models, policy gates, routes | Operating model | Candidate packet, PIR, or agent output. |
| GPT/model evaluation | Current official OpenAI docs plus evaluation gate | GPT evaluation doc | Account UI memory or model cache. |
| Context mirror | Context Mirror Runbook, registry allowlist, mirror commit | Sanitized mirror | Mirror as live runtime truth. |
| Workstreams | `config/autosint_workstreams.yml` | Generated status Markdown | `Complete` as runtime proof. |
| Archive | Manifest, archive index, replacement authorities | Git history | Archived wording as current truth. |

## Classification Rules

- `CANONICAL_RULE`: mandatory repository behavior.
- `CANONICAL_ARCHITECTURE`: durable current system structure.
- `CANONICAL_TARGET_ARCHITECTURE`: accepted target, not current runtime.
- `CANONICAL_WORKFLOW`: current operator or engineering sequence.
- `CANONICAL_RUNBOOK`: operational procedure; live claims still need receipts.
- `CANONICAL_POLICY`: durable semantic or safety policy.
- `CURRENT_IMPLEMENTATION_CONTRACT`: tracked bounded implementation behavior.
- `CURRENT_STATUS` or `GENERATED_CURRENT`: current navigation/projection, not
  live proof.
- `SUPPORTING_REFERENCE`: useful context but lower authority.
- `DESIGN_PROPOSAL` or `PROPOSAL`: target/evaluation only.
- `HISTORICAL_RECORD`, `LEGACY`, `SUPERSEDED`: provenance only.
- `CONFLICTING` or `NEEDS_OWNER_DECISION`: fail closed; do not silently
  reconcile.

## Standard Durable Header

Every registry document with `metadata_mode: standard` has exactly these
fields near its title:

```text
Status:
Authority:
Version:
Owner:
Last reviewed:
Supersedes:
Superseded by:
Runtime truth:
```

`docs/status/AUTOSINT_SYSTEM_CONTRACT_CURRENT.md` is the sole
`generated_identity` exception. Its machine-owned `Contract version`,
`Contract SHA-256`, and `Policy owner` identity remains generated by the system
contract source; duplicating a handwritten version header would create a
second contract identity. Historical records retain their meaning and add only
metadata and archival notices.

## Runtime Language

- `current` requires the applicable freshness source.
- `retained` or `stale` is continuity context, not current proof.
- `PROVEN` comes only from the canonical proof reporter.
- `app-integrated` requires registered navigation, rendered state, canonical
  data source, honest degraded/no-data states, and tests.
- `agents communicate` requires distinct identities, routing/destination,
  delivery semantics, timestamps, persisted state, provenance, read-only
  retrieval, and focused evidence.
- `accepted target` does not mean current implementation, production default,
  live health, or pilot acceptance.
- Final documentation review remains fail-closed on `WORKING_TREE_OVERRIDE`;
  a precommit override is reported, never waived.
