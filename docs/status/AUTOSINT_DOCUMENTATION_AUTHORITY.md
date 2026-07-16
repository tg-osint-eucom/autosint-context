# AUTOSINT Documentation Authority

- Status: Current
- Authority: Canonical documentation governance
- Owner: AUTOSINT Documentation
- Last reviewed: 2026-07-15
- Runtime truth: No
- Supersedes: Implicit document precedence
- Superseded by: None
- Related: [Documentation Index](AUTOSINT_DOCUMENTATION_INDEX.md), [Documentation Conflicts](AUTOSINT_DOCUMENTATION_CONFLICTS.md), [AGENTS.md](../../AGENTS.md)

## Precedence

1. Product/system safety and explicit current task scope.
2. Nearest applicable `AGENTS.override.md` or `AGENTS.md`.
3. Current tracked code, config, schemas, tests, and authoritative docs.
4. Current receipt-backed runtime reports for live-state fields.
5. Sanitized context mirror for durable recovery context only.
6. Generated audits and historical records as evidence pointers.

When documents conflict, compare authority, code/config/tests, and timestamps. Do not merge fields
from different snapshots into one apparent current state.

## Canonical Ownership Matrix

| Topic | Primary authority | Supporting authority | Not sufficient |
|---|---|---|---|
| Repository rules | `AGENTS.md` | None | Chat summaries or memory. |
| Operating model | `docs/AUTOSINT_OPERATING_MODEL_CURRENT.md` | Primary workflow | Historical reports. |
| Operator routes | `docs/AUTOSINT_PRIMARY_WORKFLOW.md` plus registered routes | API schema tests | README alone. |
| External Scout runtime | Current code, receipts, proof/health reports | External Scout Runbook | Screenshot or old receipt. |
| Scout Findings output | Current prompt contract, harvester, normalizer, runbook | Project operating model | Strict packet fixture alone. |
| Strict-packet fallback | Validator/schema and explicit fallback invocation | Evaluation dataset | Unconditional default wording. |
| Pending lifecycle | Current pending/harvester code and receipts | Runbook | Visible Stop control alone. |
| Proof semantics | Canonical proof reporter | Runbook and Long-Running Work Model | Successful-run totals. |
| Health semantics | Current health/proof report | Runbook | Route HTTP 200. |
| Operator pause | `AGENTS.md` plus current pause context/receipts | Operating model | Retained board alone. |
| Sensor architecture | Config, registry, normalizer, validator | Sensor architecture/policies | Row presence alone. |
| 13 categories | Global sensor policy and current prompt vocabulary | Sensor architecture | 19-lane count. |
| 19 lanes | `config/autosint_sensor_architecture.yml` | Sensor architecture | 52-sensor count. |
| Source status | Tracked policy/config and validator | Runbook | Free-form provider text. |
| Theater watch | Theater Watch Policy | Sensor config | Old packet. |
| Market/prediction | Market, Prediction, Finance Policy | Validator | Cue-only metric as proof. |
| Threads | `core/external_scout_threads.py` and Primary Workflow | Acceptance trace | Chat memory. |
| PIR Hunter | Current code/routes/tests and workstream | Operating model | Module existence alone. |
| Agents | Current models/code/routes/tests | Operating model | Roster or sender/thread lineage. |
| Operator Hub | Current code/read APIs | Operating model | Discovery artifact as Evidence. |
| Operator Scheduler | Current code/config and explicit approval | Workstream | UI/API status. |
| RFI | Current code/routes/tests | Operating model | Legacy workspace names. |
| RFI | Current code/routes/tests | Primary workflow | Preview as commander-ready. |
| Evidence / OSIR | Current DB models, policy gates, routes | Operating model | Candidate packet. |
| AUTOSINT.app | Registered routes, navigation, rendered tests | Primary workflow | Backend API alone. |
| Legacy routes | Registered-route absence and tests | Primary workflow | Helpers/assets/comments. |
| GPT/model evaluation | Official OpenAI docs plus evaluation gate | GPT evaluation doc | Account UI memory or model cache. |
| Context mirror | Context Mirror Runbook and mirror commit | sanitized mirror | Mirror as live runtime truth. |
| Workstreams | `config/autosint_workstreams.yml` | status Markdown | Historical notes as current proof. |

## Classification Rules

- `CANONICAL_RULE`: mandatory repository behavior.
- `CANONICAL_ARCHITECTURE`: durable current system structure.
- `CANONICAL_WORKFLOW`: current operator or engineering sequence.
- `CANONICAL_RUNBOOK`: operational procedure; live claims still need receipts.
- `CANONICAL_POLICY`: durable semantic/safety policy.
- `CURRENT_STATUS`: planning/status projection, not live runtime proof.
- `SUPPORTING_REFERENCE`: useful context but lower authority.
- `DESIGN_PROPOSAL`: target or evaluation, not implementation.
- `HISTORICAL_RECORD`, `LEGACY`, `SUPERSEDED`: retained for history only.
- `CONFLICTING` or `NEEDS_OWNER_DECISION`: do not silently reconcile.

## Standard Durable Header

New durable docs use:

```text
Status:
Authority:
Owner:
Last reviewed:
Runtime truth:
Supersedes:
Superseded by:
Related:
```

Historical evidence receives an archival notice rather than a rewrite that changes meaning.

## Runtime Language

- `current` requires the applicable freshness source.
- `retained` or `stale` is continuity context, not current proof.
- `PROVEN` comes only from the canonical proof reporter.
- A component may be `GREEN` only for its own fully proven bounded contract.
  Overall AUTOSINT readiness remains WARN/RED whenever canonical proof, source,
  contract, or runtime gates are not green; a component card never upgrades the
  overall state.
- `app-integrated` requires a registered route, navigation, rendered state, source, and tests.
- `agents communicate` requires sender, recipient/destination, delivery semantics, persisted state,
  provenance, and evidence.
