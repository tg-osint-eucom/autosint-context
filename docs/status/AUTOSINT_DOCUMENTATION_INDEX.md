# AUTOSINT Documentation Index

- Status: Current
- Authority: Canonical documentation navigation
- Owner: AUTOSINT Documentation
- Last reviewed: 2026-07-15
- Runtime truth: No; use receipts and current reports for live state
- Supersedes: Ad hoc document discovery
- Superseded by: None
- Related: [Documentation Authority](AUTOSINT_DOCUMENTATION_AUTHORITY.md), [Documentation Conflicts](AUTOSINT_DOCUMENTATION_CONFLICTS.md), [Workstreams](AUTOSINT_WORKSTREAMS.md)

## Start Here

| Path | Purpose | Authority | Owner | Status | Runtime truth | Supersedes / superseded by | Related | Reviewed |
|---|---|---|---|---|---|---|---|---|
| [AGENTS.md](../../AGENTS.md) | Safety, authority, privacy, runtime, and change rules. | `CANONICAL_RULE` | Repository governance | Current | No | Highest tracked repository rule / none | All docs | 2026-07-15 |
| [README.md](../../README.md) | Repository orientation. | `SUPPORTING_REFERENCE` | Repository | Drift review | No | None / canonical docs below | Operating model; primary workflow | 2026-07-15 |
| [System Contract](AUTOSINT_SYSTEM_CONTRACT_CURRENT.md) | Generated cross-cutting producer, transport, lifecycle, proof, model, route, and safety invariants. | `CANONICAL_RULE` | System contract | Current generated | No | Conflicting duplicated values / generated from config | Operating model; runbook | 2026-07-16 |
| [Current Operating Model](../AUTOSINT_OPERATING_MODEL_CURRENT.md) | One-shell architecture and subsystem boundaries. | `CANONICAL_ARCHITECTURE` | Architecture | Current | No | Earlier operating summaries / none | Primary workflow; runbook | 2026-07-16 |
| [Primary Workflow](../AUTOSINT_PRIMARY_WORKFLOW.md) | Current operator route sequence. | `CANONICAL_WORKFLOW` | Operator workflow | Current | No | Legacy route sequence / none | Operating model | 2026-07-15 |

## Permanent Rules

- [AGENTS.md](../../AGENTS.md): repository-wide rules and evidence hierarchy.
- [Global Sensor Coverage Policy](../AUTOSINT_GLOBAL_SENSOR_COVERAGE_POLICY.md): canonical category and source-status policy.
- [Theater Watch Policy](../AUTOSINT_THEATER_WATCH_POLICY.md): theater source requirements.
- [Market, Prediction, And Finance Policy](../AUTOSINT_MARKET_PREDICTION_FINANCE_POLICY.md): cue-only limits.
- [Trust And Assurance Model](../AUTOSINT_TRUST_AND_ASSURANCE_MODEL.md): proposed claim-level assurance contract.

## Current Architecture

| Path | Purpose | Authority | Owner | Status | Runtime truth | Supersedes / superseded by | Related | Reviewed |
|---|---|---|---|---|---|---|---|---|
| [Current Operating Model](../AUTOSINT_OPERATING_MODEL_CURRENT.md) | Current system boundaries. | `CANONICAL_ARCHITECTURE` | Architecture | Current | No | None / none | Primary workflow | 2026-07-15 |
| [Sensor Architecture](../AUTOSINT_SENSOR_ARCHITECTURE_V1.md) | Sensor/provider and packet architecture. | `CANONICAL_ARCHITECTURE` | Sensor Fabric | Drift review | No | Earlier source lists / target reference architecture does not supersede current state | Sensor policies | 2026-07-15 |
| [Lattice-Inspired Reference Architecture](../AUTOSINT_LATTICE_INSPIRED_REFERENCE_ARCHITECTURE.md) | Proposed target layers and contracts. | `DESIGN_PROPOSAL` | Architecture | Proposed | No | None / future approved architecture | Target lifecycle; trust; SLO | 2026-07-15 |
| [Target Data Lifecycle](../AUTOSINT_TARGET_DATA_LIFECYCLE.md) | Proposed source-to-review lifecycle. | `DESIGN_PROPOSAL` | Data Platform | Proposed | No | None / future approved contract | Reference architecture | 2026-07-15 |

## Primary Workflow

- [Primary Workflow](../AUTOSINT_PRIMARY_WORKFLOW.md): route and operator authority.
- [Long-Running Work Model](../AUTOSINT_LONG_RUNNING_WORK_MODEL.md): goals, proof, and continuation semantics.
- [ChatGPT/Codex Handoff Queue](../AUTOSINT_CHATGPT_CODEX_HANDOFF_QUEUE.md): tracked handoff discipline.

## External Scout

| Path | Purpose | Authority | Owner | Status | Runtime truth | Supersedes / superseded by | Related | Reviewed |
|---|---|---|---|---|---|---|---|---|
| [External Scout Runbook](../AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md) | Current production, proof, and bounded recovery contract. | `CANONICAL_RUNBOOK` | External Scout | Current | Yes, only when paired with current receipts | Earlier direct-capture schedule / none | Project operating model; primary workflow | 2026-07-16 |
| [ChatGPT Project Operating Model](../AUTOSINT_CHATGPT_PROJECT_OPERATING_MODEL.md) | Scout Findings and Project contract. | `CANONICAL_WORKFLOW` | External Scout | Current | No | Direct strict-packet default / none | Runbook | 2026-07-16 |
| [External Scout Capture Boundary](../AUTOSINT_EXTERNAL_SCOUT_CAPTURE_BOUNDARY.md) | Historical visible-capture safety boundary. | `SUPERSEDED` | External Scout | Historical | No | None / External Scout Runbook | Runbook | 2026-07-15 |

## Sensors And Sources

- [Sensor Architecture](../AUTOSINT_SENSOR_ARCHITECTURE_V1.md).
- [Global Sensor Coverage Policy](../AUTOSINT_GLOBAL_SENSOR_COVERAGE_POLICY.md).
- [Theater Watch Policy](../AUTOSINT_THEATER_WATCH_POLICY.md).
- [Market, Prediction, And Finance Policy](../AUTOSINT_MARKET_PREDICTION_FINANCE_POLICY.md).
- [Sensor Coverage Requirements Trace](../product/AUTOSINT_SENSOR_COVERAGE_REQUIREMENTS_TRACE.md): supporting historical trace, not current proof.

## Threads / Cases

- [Live Case Board Acceptance Trace](../product/AUTOSINT_LIVE_CASE_BOARD_ACCEPTANCE_TRACE.md): supporting acceptance record.
- [Case Threads Design v1](../product/AUTOSINT_CASE_THREADS_DESIGN_V1.md): superseded pre-implementation design.
- [Case Threads Buyer Questions](../product/AUTOSINT_CASE_THREADS_BUYER_QUESTIONS.md): superseded historical discovery record.
- Current route authority: [Primary Workflow](../AUTOSINT_PRIMARY_WORKFLOW.md).

## PIR

- Current truth is in [Current Operating Model](../AUTOSINT_OPERATING_MODEL_CURRENT.md): PIR backend/read APIs exist; no dedicated app surface or Thread overlay is proven.
- Future architecture constraints are in the [Reference Architecture](../AUTOSINT_LATTICE_INSPIRED_REFERENCE_ARCHITECTURE.md).

## Agents

- Current truth is in [Current Operating Model](../AUTOSINT_OPERATING_MODEL_CURRENT.md): Agent storage/read APIs and gated writes exist; recipient/delivery proof does not.
- Interview and audit criteria are in the [Architecture Audit Question Bank](../AUTOSINT_ARCHITECTURE_AUDIT_QUESTION_BANK.md).

## RFI

- [Primary Workflow](../AUTOSINT_PRIMARY_WORKFLOW.md): route and preview-only authority.
- [Current Operating Model](../AUTOSINT_OPERATING_MODEL_CURRENT.md): thread-current selection and safety boundary.

## Operator UI

- [Primary Workflow](../AUTOSINT_PRIMARY_WORKFLOW.md): one-shell navigation.
- [Live Case Board Acceptance Trace](../product/AUTOSINT_LIVE_CASE_BOARD_ACCEPTANCE_TRACE.md): supporting UI acceptance record.
- `/moltbook`, `/dagrbook`, and `/control-plane` are legacy removed, not UI destinations.

## Runtime Operations

- [External Scout Runbook](../AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md).
- [Context Mirror Runbook](../AUTOSINT_CONTEXT_MIRROR_RUNBOOK.md).
- [Long-Running Work Model](../AUTOSINT_LONG_RUNNING_WORK_MODEL.md).

## Proof And Health

- External Scout proof: [External Scout Runbook](../AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md).
- Goal proof language: [Long-Running Work Model](../AUTOSINT_LONG_RUNNING_WORK_MODEL.md).
- Live truth comes from current reports and receipts, not this index.

## Evaluation And Models

- [Evaluation Dataset](../AUTOSINT_EVALUATION_DATASET_V0.md): evaluation contract.
- [GPT-5.6 Model Upgrade Evaluation](../AUTOSINT_GPT56_MODEL_UPGRADE_EVALUATION.md): evaluation-only; no migration approval.
- `tests/fixtures/autosint_eval/*.md`: active test fixtures, not documentation authority.

## Security And Safety

- [AGENTS.md](../../AGENTS.md).
- [Trust And Assurance Model](../AUTOSINT_TRUST_AND_ASSURANCE_MODEL.md).
- [Context Mirror Runbook](../AUTOSINT_CONTEXT_MIRROR_RUNBOOK.md).

## Workstreams

- [Workstreams](AUTOSINT_WORKSTREAMS.md): concise current projection from the
  structured registry. Historical runtime narratives are not current proof.
- `config/autosint_workstreams.yml`: structured source for workstream rows.

## Working-Tree Drift

This durable index describes committed authority and document state. It does
not encode transient dirty/override status. The final documentation review
package records `HEAD`, `WORKING_TREE_OVERRIDE`, both SHA-256 values, and the
source commit separately.

## ADRs / Design Proposals

- [Orchestration Roadmap](../AUTOSINT_ORCHESTRATION_ROADMAP.md).
- [Lattice-Inspired Reference Architecture](../AUTOSINT_LATTICE_INSPIRED_REFERENCE_ARCHITECTURE.md).
- [Architecture Audit Question Bank](../AUTOSINT_ARCHITECTURE_AUDIT_QUESTION_BANK.md).
- [Expert Architecture Interview Guide](../AUTOSINT_EXPERT_ARCHITECTURE_INTERVIEW_GUIDE.md).
- [Target Data Lifecycle](../AUTOSINT_TARGET_DATA_LIFECYCLE.md).
- [Trust And Assurance Model](../AUTOSINT_TRUST_AND_ASSURANCE_MODEL.md).
- [Latency And Resilience SLO](../AUTOSINT_LATENCY_AND_RESILIENCE_SLO.md).

No ADR directory convention exists. Proposed decisions remain in the reference architecture until
an ADR convention is approved.

## Historical / Superseded

- [External Scout Capture Boundary](../AUTOSINT_EXTERNAL_SCOUT_CAPTURE_BOUNDARY.md).
- [Case Threads Design v1](../product/AUTOSINT_CASE_THREADS_DESIGN_V1.md).
- [Case Threads Buyer Questions](../product/AUTOSINT_CASE_THREADS_BUYER_QUESTIONS.md).
- Historical receipt narratives inside current docs remain history and cannot prove live state.

## Legacy

MOLTBook, DAGRBook, and Control Plane names may appear in historical records, test helpers, assets,
or provenance. Their browser routes are removed. Do not treat residue as implementation.

## Generated Artifacts

Generated audit and runtime artifacts are not tracked documentation authority. The current
architecture/documentation audit is under:

`artifacts/operator_reading/latest/lattice_docs_architecture_audit/`

Runtime reports must be checked by timestamp and cannot be inferred from this durable index.
