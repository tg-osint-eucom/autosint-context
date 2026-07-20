# AUTOSINT Current State

- Status: Current tracked implementation classification
- Authority: Repository-state navigation; code/config/tests and current receipts remain field authorities
- Version: 2.1
- Owner: AUTOSINT Architecture and Operations
- Last reviewed: 2026-07-20
- Supersedes: Subsystem state inferred from scattered design documents
- Superseded by: None
- Runtime truth: No; live health, data, proof, and release claims require current receipt-backed reporters
- Related: [Documentation Authority](AUTOSINT_DOCUMENTATION_AUTHORITY.md), [Architecture Decisions V2.1](../architecture/AUTOSINT_ARCHITECTURE_DECISIONS_V2_1.md), [Workstreams](AUTOSINT_WORKSTREAMS.md), [Production Architecture V2.1](../architecture/AUTOSINT_PRODUCTION_ARCHITECTURE_V2_1.md)

This page separates repository implementation from live runtime and from the
accepted V2.1 target. A tracked implementation, registered route, passing test,
or HTTP 200 does not by itself prove current data, service health, production
acceptance, or release readiness.

## Current Repository Implementation

| Area | Repository classification | What is currently established | What is not established |
|---|---|---|---|
| External Scout | `CURRENT_PRODUCTION_DEFAULT` | The browser-backed Scout Findings lifecycle, deterministic normalization/validation, Threads, RFI preview, and canonical same-source proof boundary remain the current production default. | Production Foundation V2.1 does not switch the provider, prompt schedule, proof source, or promotion authority. |
| PostgreSQL | `ISOLATED_LOCAL_RUNTIME_VALIDATED` | The operator-approved preservation gate targets only the labelled loopback development/test container and volume. The pinned image, revision `20260719_0004`, 35-table `public` inventory, required extensions, reconnect, and synthetic backup/restore passed in the pre-push review. | Default behavior remains `EXISTING_DATABASE_REQUIRES_OPERATOR_DECISION`; the detected unmanaged host PGDATA remains untouched and unused. No production database, production data, destructive reset, or pilot authority is approved. |
| Collection/capabilities | `GENERATED_CURRENT_INVENTORY` | The V2.1 registry deterministically inventories capabilities, source rows, 13 canonical categories, and 19 operational lanes. A specialized safe GET projection exposes registry provenance and current-evidence conflicts. | Inventory presence is not current collection proof; the current projection is honestly `DEGRADED` while most rows lack compatible current receipt-backed evidence. |
| PIR Hunter | `REGISTERED_READ_ONLY_REPLAY` | Dedicated PIR contracts, advisory repository/service behavior, applied schemas/migrations, GET routes, gated write routes, and canonical-app router registration exist. Synthetic PostgreSQL PIR persistence passed against the isolated target. The default canonical-app service remains deterministic read-only replay. | No current operational PostgreSQL PIR dataset, authenticated operator CRUD acceptance, production automation, Evidence/case/source mutation, or independent answer authority is proven. |
| Agent Runtime | `REGISTERED_GET_ONLY_WITH_SQL_SMOKE` | A manager-controlled typed runtime, append-only event-store contracts, applied migrations, deterministic replay, canonical-app GET routes, and isolated PostgreSQL event-store persistence/reconnect smoke exist. | Production mode and OpenAI staging remain disabled. Synthetic persistence does not grant Agent Evidence/case/source/Thread mutation authority or prove autonomous production communication. |
| Agent Collaboration Room | `CURRENT_READ_PROJECTION_AND_LABELLED_FIXTURE` | The same server exposes a read-only human-readable projection over persisted typed events and a separately selected demo whose source state remains `DETERMINISTIC_REPLAY_FIXTURE`. | Persisted storage and routing fields do not prove autonomous peer operation, production delivery, or mutation authority. |
| ScoutGenerationService | `REPLAY_ONLY` | API-neutral task/result/event contracts and deterministic test providers exist. | No production queue, worker, OpenAI call, browser control, canonical app API, or production-default switch exists. |
| MCP | `MCP_CANONICAL_READONLY_PROVEN` | The canonical repository server contract is read-only by default, write gates are off, a bounded rebind/handshake was proven without a write call, and `/api/v1/system/mcp` exposes only safe gate/inventory provenance. | Tool/API availability does not authorize mutation or prove an external live handshake; later sessions must revalidate current registration and gates before relying on it. |
| Operator UI V2 | `DEFAULT_OFF_CODEX_RENDERED_UAT_PASS` | One same-server local-only preview shell implements `MISSION`, `WATCH`, `CASES`, `PIR`, `AGENTS`, `RFI`, and `SYSTEM` behind a default-off flag. Canonical MISSION/CASES state fidelity, specialized System projections, real keyboard traversal, desktop/mobile containment, and screenshot integrity passed the scoped Codex rendered harness. | It is not the production default; human operator UAT, staging soak, and production acceptance are not claimed. |
| Archive/cleanup | `SAFE_ARCHIVE_PRECOMMIT` | Three proven-superseded documents have planned tracked move pairs with a manifest and rebound inbound references. | The move is not HEAD authority until the coordinated commit; no `DEAD_CONFIRMED` deletion is authorized. |
| Pilot acceptance | `HOLD` | Acceptance policy, release procedure, incident plan, soak plan, matrix, and checklist exist. | Full production readiness, SOCOM production authorization, ATO, and pilot go-live are not claimed. |

## Target State

The accepted target is a production-grade foundation for a controlled SOCOM
pilot:

```text
Operator App
-> Mission/PIR Control Plane
-> typed task queue
-> manager-controlled Agent Runtime
-> Sensor/Adapter Plane
-> Validation and Provenance
-> PostgreSQL Data Plane
-> canonical APIs
-> authenticated Human Approval Boundary
```

The target is `TARGET_NOT_ACCEPTED`. It remains one application, one External
Scout proof source, one Live Board, and one case-memory system. Provider
migration, production database selection, authentication/RBAC, live queue and
worker operation, staging soak, operator UAT, and the acceptance matrix must
pass before target documents can become production runtime truth.

## Snapshot And Proof Rules

- Repository implementation, live server state, PostgreSQL state, MCP
  registration, External Scout proof, and acceptance gates are separate
  snapshots.
- Current runtime claims use the newest applicable timestamped receipt or
  canonical reporter; this document never upgrades retained or stale data.
- A working-tree implementation is not committed authority. Final
  documentation review remains fail-closed on `WORKING_TREE_OVERRIDE` until
  the exact coordinated commit exists.
- Optional OpenAI providers remain disabled; this program made no API call and
  read no credential value.
- The isolated PostgreSQL and rendered UI results are bounded pre-push
  acceptance snapshots. The final ignored review packet records their exact
  timestamps and hashes; this navigation page is not a replacement for those
  receipts.
