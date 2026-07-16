# AUTOSINT Lattice-Inspired Reference Architecture

- Status: Proposed
- Authority: Target architecture proposal
- Owner: AUTOSINT Architecture
- Last reviewed: 2026-07-15
- Runtime truth: No; this document does not claim implementation
- Supersedes: None
- Superseded by: None
- Related: [Current Operating Model](AUTOSINT_OPERATING_MODEL_CURRENT.md), [Target Data Lifecycle](AUTOSINT_TARGET_DATA_LIFECYCLE.md), [Trust And Assurance Model](AUTOSINT_TRUST_AND_ASSURANCE_MODEL.md), [Architecture Audit Question Bank](AUTOSINT_ARCHITECTURE_AUDIT_QUESTION_BANK.md)

## Decision

Evolve AUTOSINT as one read-only operator platform around versioned canonical events,
deterministic validation, temporal provenance, bounded analysis, and explicit degraded modes.
Public Lattice material is used only as an architectural comparison.

Directly documented public Lattice themes used here are local/edge operation,
operation across intermittent networks, standardized/open data exchange, and
interoperability. AUTOSINT-derived design choices are versioned provenance,
claim lifecycle, deterministic promotion gates, explicit degraded states, and
human supervision. Those derived choices are not attributed to Lattice.

This is not a Lattice implementation, integration, compatibility claim, or copy of proprietary
internals.

## Non-Negotiable Boundary

- one AUTOSINT.app shell;
- one External Scout proof source;
- Threads remains durable case memory;
- RFI remains analyst preview only;
- LLM output remains proposed/candidate state;
- graph edges remain proposed until deterministic validation or human approval;
- PIRs remain advisory;
- agents remain bounded;
- operator UI remains read-only;
- Evidence, OSIR, apply/import, and commander-ready authority remain closed.

## Target Layers

### 1. Sensor Fabric

Owns provider capabilities, source policy, status, collection timestamps, reliability, cost, and
lane budgets. It emits versioned canonical sensor events; it does not write Evidence or active
case state.

### 2. Adapter Boundary

Provider-specific parsing, authentication status, rate limits, and field mapping end here. Every
adapter passes a conformance suite and emits the same envelope or a typed failure. A new provider
must not require downstream UI, proof, Thread, or RFI changes.

### 3. Event Bus / Queue

A future queue contract owns ordering, dedupe, backpressure, priority, defer/drop accounting,
replay, and persistence. No implementation or dependency is selected by this document.

### 4. Fast Triage Lane

Deterministic rules and inexpensive local methods classify, deduplicate, score freshness, protect
quiet anomalies, and route selected events. It remains available when frontier models are not.

### 5. Deep Analysis Lane

Selected candidate events receive bounded model-assisted synthesis. Every run records scope,
inputs, exclusions, model/version, prompt contract, budget, timeout, and result. Output cannot
bypass deterministic validation.

### 6. Temporal Provenance Graph

The logical contract represents `Entity`, `Event`, `Claim`, `Observation`, `Source`,
`SensorCheck`, `Relationship`, `CaseThread`, `PIR`, `Decision`, `Receipt`, and `Artifact`.
Relationships carry temporal validity, source/evidence references, confidence basis,
contradiction, validation state, proposer, and approver.

This is a logical contract first. No graph database is selected.

### 7. Retrieval Layer

Deterministic lookup and bounded traversal come first. Vector retrieval and
GraphRAG are `EVALUATE_LATER` options after identity, provenance, retraction,
citation reconstruction, and replay are proven. Canonical event and provenance
contracts come first. Retrieval must return supporting and contradicting paths
and state traversal limits.

### 8. PIR / Mission Question Layer

PIRs express advisory priorities and map questions to sources, observations, claims, and Threads.
They cannot redefine External Scout proof, Evidence, OSIR, case links, or commander-ready state.

### 9. Agent Orchestration Layer

Any future agent task requires sender, recipient/destination, task type, delivery state, budget,
timeout, idempotency, provenance, tool authority, result, and terminal status. Multiple agents do
not substitute for independent validation. Writes remain separately gated.

### 10. Deterministic Validation Layer

Validates event schemas, provenance, required lanes, cue-only policy, temporal consistency,
relationship evidence, candidate freshness, and promotion gates. Invalid or ambiguous state fails
closed and remains visible as candidate/quarantined/unavailable.

### 11. Thread / Case Memory

Threads keep stable topic identity, lineage, strongest current state, retained/stale state,
contradictions, collection gaps, and next checks. Candidate updates may append without replacing
stronger current state.

### 12. Operator Common Operating Picture

Mission Control, External Scout, Threads, Proof Data, and RFI remain one shell.
Views consume canonical projections and show current, retained, stale, unavailable, blocked,
planned, and gated states explicitly.

### 13. Proof / Health / Receipts

Every stage emits bounded receipts. Proof remains same-source and natural-cycle based. Health
reports dependency, queue, freshness, validation, promotion, and operator-view state without
turning WARN or retained data into GREEN.

### 14. Deployment / Edge / Degraded Plane

Defines local continuity, store-and-forward, replay, state reconciliation, and no-network,
no-model, no-DB, no-browser, and partial-adapter behavior. Last-known-good data is retained only
with honest stale labels.

### 15. Policy / Security Plane

Defines data classification/residency, least authority, privacy, encryption/key boundary, signed
artifacts, dependency/SBOM policy, offline updates, cue-only policy, and mutation gates.

## Default Flow

```text
Sources
  -> Adapters
  -> Canonical Sensor Events
  -> Fast Triage
  -> Priority Queue
  -> Deep Analysis
  -> Claim / Observation / Relationship Proposals
  -> Deterministic Validation
  -> Temporal Provenance Graph
  -> Threads / PIR
  -> External Scout / Mission Control / RFI
  -> Human Review
```

Cross-cutting fields: provenance, receipts, health, data residency, cue-only policy,
mutation gates, model/version identity, and degraded mode.

## Canonical Sensor Event Envelope

The future versioned envelope should include:

- `event_id`, `schema_version`, `sensor_id`, `operational_lane`, `canonical_category`;
- `source_id`, `provider_id`, `source_url`, `source_artifact_ref`;
- `observed_at`, `published_at`, `ingested_at`, `expires_at`;
- `status`, `freshness_state`, `cue_only`, `proof_capable`;
- `payload`, `payload_hash`, `normalization_version`;
- `provenance`, `confidence_basis`, `collection_gap`, `next_check`;
- `trace_id`, `parent_event_ids`, `receipt_refs`.

Unknown fields must be preserved or rejected by an explicit version policy, never silently lost.

## Proposed Decision Sequence

1. Approve the logical sensor-event and temporal-provenance contracts.
2. Build golden raw-to-canonical and canonical-to-UI replays.
3. Instrument queue, preservation, traceability, latency, and degraded-mode metrics.
4. Prove provider replacement and 100x synthetic replay.
5. Evaluate storage and queue implementations from measured requirements.
6. Evaluate GraphRAG only after trusted edge state exists.
7. Evaluate agent transport only after recipient/delivery and independent-validation contracts.

## Explicitly Not Implemented Here

- graph or vector database;
- event bus or queue product;
- new agent transport;
- new app route, dashboard, or server;
- DB schema change;
- model deployment or default change;
- source, Evidence, OSIR, apply/import, or commander-ready mutation.

Each requires a separate goal, approval, migration plan, tests, and runtime proof.
