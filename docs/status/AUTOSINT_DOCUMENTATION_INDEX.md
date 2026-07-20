# AUTOSINT Documentation Index

- Status: Current
- Authority: Canonical documentation navigation
- Version: 2.1
- Owner: AUTOSINT Documentation
- Last reviewed: 2026-07-20
- Supersedes: Ad hoc document discovery and mixed current/target navigation
- Superseded by: None
- Runtime truth: No; use current receipts and field-authoritative reporters for live state
- Related: [Documentation Authority](AUTOSINT_DOCUMENTATION_AUTHORITY.md), [Documentation Conflicts](AUTOSINT_DOCUMENTATION_CONFLICTS.md), [Current State](AUTOSINT_CURRENT_STATE.md), [Workstreams](AUTOSINT_WORKSTREAMS.md)

`config/autosint_documentation_authority.yml` is the machine-readable inventory
behind this page. This index explicitly separates current repository
implementation, target architecture, proposals, generated projections, and
history. It does not merge them into one snapshot.

## Start Here

| Path | Use | Truth boundary |
|---|---|---|
| [AGENTS.md](../../AGENTS.md) | Repository constitution and evidence hierarchy. | Rules, not runtime proof. |
| [AUTOSINT_DOCUMENTATION_AUTHORITY.md](AUTOSINT_DOCUMENTATION_AUTHORITY.md) | Precedence, ownership, metadata, and language rules. | Documentation governance. |
| [AUTOSINT_CURRENT_STATE.md](AUTOSINT_CURRENT_STATE.md) | Current repository implementation versus target and live runtime. | Navigation; field evidence still wins. |
| [AUTOSINT_SYSTEM_CONTRACT_CURRENT.md](AUTOSINT_SYSTEM_CONTRACT_CURRENT.md) | Machine-generated cross-cutting contract identity. | Generated identity; not live proof. |
| [AUTOSINT_OPERATING_MODEL_CURRENT.md](../AUTOSINT_OPERATING_MODEL_CURRENT.md) | Current one-shell architecture and subsystem boundaries. | Current architecture. |
| [AUTOSINT_PRIMARY_WORKFLOW.md](../AUTOSINT_PRIMARY_WORKFLOW.md) | Current operator route sequence. | Current workflow. |
| [AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md](../AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md) | Current External Scout lifecycle and proof procedure. | Pair with current receipts. |
| [AUTOSINT_ARCHITECTURE_DECISIONS_V2_1.md](../architecture/AUTOSINT_ARCHITECTURE_DECISIONS_V2_1.md) | Accepted V2.1 target decisions. | Target decisions, not acceptance. |
| [AUTOSINT_PRODUCTION_ARCHITECTURE_V2_1.md](../architecture/AUTOSINT_PRODUCTION_ARCHITECTURE_V2_1.md) | Consolidated V2.1 target architecture. | Target state. |
| [AUTOSINT_WORKSTREAMS.md](AUTOSINT_WORKSTREAMS.md) | Generated durable planning projection. | Planning, not runtime proof. |

## Current Repository State

These documents describe current rules, tracked implementation contracts, or
generated current inventories. Current runtime still requires the applicable
receipt, route/data smoke, health reporter, or proof reporter.

### Core workflow and policy

- [AUTOSINT_CHATGPT_PROJECT_OPERATING_MODEL.md](../AUTOSINT_CHATGPT_PROJECT_OPERATING_MODEL.md)
- [AUTOSINT_SENSOR_ARCHITECTURE_V1.md](../AUTOSINT_SENSOR_ARCHITECTURE_V1.md)
- [AUTOSINT_GLOBAL_SENSOR_COVERAGE_POLICY.md](../AUTOSINT_GLOBAL_SENSOR_COVERAGE_POLICY.md)
- [AUTOSINT_THEATER_WATCH_POLICY.md](../AUTOSINT_THEATER_WATCH_POLICY.md)
- [AUTOSINT_MARKET_PREDICTION_FINANCE_POLICY.md](../AUTOSINT_MARKET_PREDICTION_FINANCE_POLICY.md)
- [AUTOSINT_LONG_RUNNING_WORK_MODEL.md](../AUTOSINT_LONG_RUNNING_WORK_MODEL.md)
- [AUTOSINT_CHATGPT_CODEX_HANDOFF_QUEUE.md](../AUTOSINT_CHATGPT_CODEX_HANDOFF_QUEUE.md)
- [AUTOSINT_CONTEXT_MIRROR_RUNBOOK.md](../AUTOSINT_CONTEXT_MIRROR_RUNBOOK.md)
- [EXTERNAL_SCOUT_PROJECT_INSTRUCTIONS_SYNC.md](EXTERNAL_SCOUT_PROJECT_INSTRUCTIONS_SYNC.md)

### Generated and supporting current views

- [AUTOSINT_CAPABILITY_REGISTRY_CURRENT.md](AUTOSINT_CAPABILITY_REGISTRY_CURRENT.md)
- [AUTOSINT_COLLECTION_PLANE_CURRENT.md](AUTOSINT_COLLECTION_PLANE_CURRENT.md)
- [AUTOSINT_DOCUMENTATION_CONFLICTS.md](AUTOSINT_DOCUMENTATION_CONFLICTS.md)
- [AUTOSINT_DOCUMENTATION_INDEX.md](AUTOSINT_DOCUMENTATION_INDEX.md)
- [AUTOSINT_LIVE_CASE_BOARD_ACCEPTANCE_TRACE.md](../product/AUTOSINT_LIVE_CASE_BOARD_ACCEPTANCE_TRACE.md)
- [AUTOSINT_SENSOR_COVERAGE_REQUIREMENTS_TRACE.md](../product/AUTOSINT_SENSOR_COVERAGE_REQUIREMENTS_TRACE.md)

### Current bounded implementation contracts

- [AUTOSINT_MCP_BOUNDARY_V1.md](../architecture/AUTOSINT_MCP_BOUNDARY_V1.md):
  canonical repository, read-only default, explicit exceptional write gates;
  current rebind proof remains receipt-backed.
- [AUTOSINT_SCOUT_GENERATION_SERVICE_V1.md](../architecture/AUTOSINT_SCOUT_GENERATION_SERVICE_V1.md):
  typed replay-only foundation; no production provider/default switch.
- [AUTOSINT_POSTGRES_LOCAL_DEVELOPMENT.md](../operations/AUTOSINT_POSTGRES_LOCAL_DEVELOPMENT.md):
  loopback-only local development/test foundation with an explicit two-part
  preserved-PGDATA exception; no production target approval.
- [AUTOSINT_DATABASE_MIGRATIONS.md](../operations/AUTOSINT_DATABASE_MIGRATIONS.md):
  ordered forward-only `public` migration authority and isolated-target
  acceptance boundary.
- [AUTOSINT_DATABASE_BACKUP_AND_RESTORE.md](../operations/AUTOSINT_DATABASE_BACKUP_AND_RESTORE.md):
  integrity-compared synthetic local backup/restore contract, not production
  backup/restore authority.

## Target Architecture

These documents define accepted target boundaries or partially implemented
target surfaces. They do not replace the current production default and do not
prove pilot acceptance.

| Path | Target role | Current boundary |
|---|---|---|
| [AUTOSINT_CONTROL_PLANE_V2.md](../architecture/AUTOSINT_CONTROL_PLANE_V2.md) | Mission/PIR/task authority boundaries. | Target; current registered behavior is classified separately. |
| [AUTOSINT_AGENT_RUNTIME_V1.md](../architecture/AUTOSINT_AGENT_RUNTIME_V1.md) | Manager-controlled typed agent runtime. | Partial target; deterministic replay and GET projections only by default. |
| [AUTOSINT_PIR_HUNTER_V1.md](../architecture/AUTOSINT_PIR_HUNTER_V1.md) | Dedicated advisory PIR domain. | Partial target; default canonical service is read-only replay. |
| [AUTOSINT_AGENT_COLLABORATION_ROOM_V1.md](../architecture/AUTOSINT_AGENT_COLLABORATION_ROOM_V1.md) | Human-readable typed collaboration projection. | Partial target; demo fixtures are not live communication proof. |
| [AUTOSINT_SENSOR_AND_COLLECTION_PLANE_V2.md](../architecture/AUTOSINT_SENSOR_AND_COLLECTION_PLANE_V2.md) | Sensor/adapter target. | Inventory and provider implementation vary by row. |
| [AUTOSINT_VALIDATION_AND_PROVENANCE_V2.md](../architecture/AUTOSINT_VALIDATION_AND_PROVENANCE_V2.md) | Validation/provenance target. | Target; current canonical validators remain authoritative. |
| [AUTOSINT_DATA_PLANE_V2.md](../architecture/AUTOSINT_DATA_PLANE_V2.md) | PostgreSQL data-plane target. | Isolated development/test migration and recovery proof obtained; no production target approved. |
| [AUTOSINT_OBSERVABILITY_PLANE_V1.md](../architecture/AUTOSINT_OBSERVABILITY_PLANE_V1.md) | Health/audit/metrics target. | Target; existing canonical reporters remain authoritative. |
| [AUTOSINT_OPERATOR_UI_V2.md](../architecture/AUTOSINT_OPERATOR_UI_V2.md) | One same-server operator shell. | Default-off local GET-only preview with scoped `CODEX_RENDERED_UAT_PASS`; human UAT and production acceptance remain pending. |
| [AUTOSINT_SECURITY_AND_DEPLOYMENT_V2.md](../architecture/AUTOSINT_SECURITY_AND_DEPLOYMENT_V2.md) | Auth/RBAC/deployment target. | Target; no production authorization claimed. |
| [AUTOSINT_MIGRATION_FROM_BROWSER_RUNTIME.md](../architecture/AUTOSINT_MIGRATION_FROM_BROWSER_RUNTIME.md) | Explicit provider migration gates. | Target; browser-backed Scout remains production default. |
| [AUTOSINT_OPERATOR_INFORMATION_HIERARCHY_V2.md](../product/AUTOSINT_OPERATOR_INFORMATION_HIERARCHY_V2.md) | Target operator information hierarchy. | Partial target; acceptance requires route/browser/UAT evidence. |

## Operations And Acceptance

- [AUTOSINT_PRODUCTION_ACCEPTANCE.md](../operations/AUTOSINT_PRODUCTION_ACCEPTANCE.md):
  gate policy; a document or passing unit suite is not acceptance.
- [AUTOSINT_RELEASE_RUNBOOK.md](../operations/AUTOSINT_RELEASE_RUNBOOK.md):
  bounded release procedure.
- [AUTOSINT_INCIDENT_RESPONSE.md](../operations/AUTOSINT_INCIDENT_RESPONSE.md):
  incident classification and safe response.
- [AUTOSINT_STAGING_SOAK_PLAN.md](../operations/AUTOSINT_STAGING_SOAK_PLAN.md):
  proposed staging soak; no soak claimed.

## Design And Evaluation Proposals

- [AUTOSINT_EVALUATION_DATASET_V0.md](../AUTOSINT_EVALUATION_DATASET_V0.md)
- [AUTOSINT_GPT56_MODEL_UPGRADE_EVALUATION.md](../AUTOSINT_GPT56_MODEL_UPGRADE_EVALUATION.md)
- [AUTOSINT_ORCHESTRATION_ROADMAP.md](../AUTOSINT_ORCHESTRATION_ROADMAP.md)
- [AUTOSINT_LATTICE_INSPIRED_REFERENCE_ARCHITECTURE.md](../AUTOSINT_LATTICE_INSPIRED_REFERENCE_ARCHITECTURE.md)
- [AUTOSINT_TARGET_DATA_LIFECYCLE.md](../AUTOSINT_TARGET_DATA_LIFECYCLE.md)
- [AUTOSINT_TRUST_AND_ASSURANCE_MODEL.md](../AUTOSINT_TRUST_AND_ASSURANCE_MODEL.md)
- [AUTOSINT_LATENCY_AND_RESILIENCE_SLO.md](../AUTOSINT_LATENCY_AND_RESILIENCE_SLO.md)

Proposal metadata is explicit. A proposal does not become current because code
with a similar name exists.

## Historical And Superseded

- [README.md](../history/README.md): documentation-history root.
- [superseded/README.md](../history/superseded/README.md): superseded-document index.
- [AUTOSINT_EXTERNAL_SCOUT_CAPTURE_BOUNDARY.md](../history/superseded/AUTOSINT_EXTERNAL_SCOUT_CAPTURE_BOUNDARY.md):
  historical direct-capture boundary, superseded by the current runbook.
- [AUTOSINT_CASE_THREADS_DESIGN_V1.md](../history/superseded/AUTOSINT_CASE_THREADS_DESIGN_V1.md):
  historical pre-implementation design.
- [AUTOSINT_CASE_THREADS_BUYER_QUESTIONS.md](../history/superseded/AUTOSINT_CASE_THREADS_BUYER_QUESTIONS.md):
  historical discovery input.
- [incidents/README.md](../history/incidents/README.md): empty tracked incident archive section.
- [migrations/README.md](../history/migrations/README.md): empty tracked historical-migration section.

The archive manifest preserves original paths and hashes. Archived text is
provenance, never current runtime or implementation authority.

## Working-Tree And Mirror Boundary

- Final documentation consistency remains fail-closed when any review corpus
  document is a `WORKING_TREE_OVERRIDE`; precommit overrides are expected and
  reported separately, not treated as committed authority.
- Mirror inputs are the registry rows with `mirror_input: true`, plus the
  bounded base/generated/config files declared by the publisher.
- The public mirror contains sanitized committed recovery context only. It
  cannot prove current launchd, browser, database, packet, thread, proof, MCP,
  or route state.
- `/moltbook`, `/dagrbook`, and `/control-plane` remain legacy removed. Names in
  history, assets, helpers, or config do not restore those routes.
