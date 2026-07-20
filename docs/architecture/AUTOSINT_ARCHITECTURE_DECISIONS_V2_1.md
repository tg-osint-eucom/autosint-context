# AUTOSINT Architecture Decisions V2.1

- Status: Current accepted target-decision register
- Authority: Production Foundation V2.1 architecture decisions
- Version: 2.1
- Owner: AUTOSINT Architecture
- Last reviewed: 2026-07-19
- Supersedes: Unnumbered V2.1 decisions scattered across proposals and phase notes
- Superseded by: None
- Runtime truth: NO — accepted target decisions do not prove implementation, live health, migration, or pilot acceptance
- Related: [Current State](../status/AUTOSINT_CURRENT_STATE.md), [Production Architecture V2.1](AUTOSINT_PRODUCTION_ARCHITECTURE_V2_1.md), [Documentation Authority](../status/AUTOSINT_DOCUMENTATION_AUTHORITY.md)

These decisions define the accepted target and authority boundaries. The
current repository/runtime classification remains in `AUTOSINT_CURRENT_STATE`;
acceptance requires the independent production gates.

| Decision | Status | Decision | Current implementation boundary | Supersedes |
|---|---|---|---|---|
| `V21-ADR-001` | `ACCEPTED` | Preserve one AUTOSINT server/application shell, one External Scout proof source, one Live Board, and one case-memory system. | UI V2 is a default-off same-server preview; current External Scout routes remain primary. | Competing dashboard or second-app proposals. |
| `V21-ADR-002` | `ACCEPTED` | Preserve the browser-backed External Scout lifecycle as the production default until explicit migration acceptance. | ScoutGenerationService is replay-only and no OpenAI/browser provider is enabled. | Implicit provider or prompt-default changes. |
| `V21-ADR-003` | `ACCEPTED` | Use one forward-only PostgreSQL migration chain in schema `public`; keep unresolved `idos.*` compatibility fail-closed and read-only. | Offline migrations exist; no service or migration receipt exists because the unknown existing-data stop condition remains. | Opportunistic runtime DDL and parallel schema authority. |
| `V21-ADR-004` | `ACCEPTED` | Implement PIR Hunter as a dedicated advisory mission/question and collection-gap domain. | Read-only replay and gated routes exist; PIR cannot mutate Evidence, cases, sources, OSIR, apply/import, proof, or commander-ready state. | PIR status inferred from model text or legacy write-capable orchestration. |
| `V21-ADR-005` | `ACCEPTED` | Use manager-controlled typed Agent orchestration with an append-only event store and bounded handoffs. | Deterministic replay and GET-only canonical-app projections exist; production/OpenAI modes remain disabled. | Unbounded peer chat and roster-only communication claims. |
| `V21-ADR-006` | `ACCEPTED` | Keep OpenAI Agents and Responses adapters optional, disabled, and credential-free until separately approved replay/staging gates pass. | Fake/replay contract tests only; no API call or key read is authorized. | Provider availability inferred from product announcements, account UI, or model cache. |
| `V21-ADR-007` | `ACCEPTED` | Bind MCP to the canonical repository, default it read-only, and require global, class, per-call, scope, policy, and receipt gates for every exceptional write. | Canonical read-only rebind/handshake is proven; all write gates were off. | Legacy checkout binding and single-flag write authorization. |
| `V21-ADR-008` | `ACCEPTED` | Introduce operator UI V2 only as a local, GET-only, default-off preview until QA/UAT/acceptance. | Preview tabs consume canonical APIs in the existing server; no second truth source or write controls. | Immediate replacement of current operator routes. |
| `V21-ADR-009` | `ACCEPTED` | Archive only proven-superseded tracked material; delete only `DEAD_CONFIRMED` material after deterministic reference and validation gates. | Three Phase 13 moves are prepared; zero dead-file deletion is authorized. | Name-based cleanup and destructive ignored-artifact cleanup. |
| `V21-ADR-010` | `ACCEPTED` | Publish only committed, allowlisted, sanitized documentation/config context to the public mirror. | Mirror inputs are selected by the documentation-authority registry; dry-run is non-mutating and publication remains a later phase. | Mirror content inferred from an ad hoc hard-coded documentation list. |

## Decision Use

- `ACCEPTED` means the target boundary is approved for this program; it does
  not mean the target is implemented or operationally proven.
- If current code and a target decision differ, the current production default
  remains authoritative until its migration/acceptance gate passes.
- A future decision must use a new ID, state what it supersedes, update the
  documentation authority registry/index/conflict register, and preserve
  historical provenance.
