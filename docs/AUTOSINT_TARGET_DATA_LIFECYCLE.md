# AUTOSINT Target Data Lifecycle

- Status: Proposed
- Authority: Target data contract proposal
- Owner: AUTOSINT Data Platform
- Last reviewed: 2026-07-15
- Runtime truth: No; target state only
- Supersedes: None
- Superseded by: None
- Related: [Reference Architecture](AUTOSINT_LATTICE_INSPIRED_REFERENCE_ARCHITECTURE.md), [Sensor Architecture](AUTOSINT_SENSOR_ARCHITECTURE_V1.md), [Trust And Assurance Model](AUTOSINT_TRUST_AND_ASSURANCE_MODEL.md)

## Objective

Make every operator conclusion reconstructible from source through collection, normalization,
validation, analysis, thread selection, and human review without silently losing provider fields
or granting candidate data production authority.

## State Machine

```text
DISCOVERED
  -> COLLECTED
  -> CANONICALIZED
  -> TRIAGED
  -> ANALYSIS_PROPOSED
  -> VALIDATED_CANDIDATE
  -> THREAD_ELIGIBLE
  -> OPERATOR_REVIEWED
```

Side states:

```text
NOT_CHECKED | BLOCKED | STALE | DEFERRED | DUPLICATE | QUARANTINED |
RETRACTED | SUPERSEDED | UNAVAILABLE
```

No state in this lifecycle is automatically `Evidence`, `OSIR`, `apply/import`, or
`commander-ready`.

## Stage Contracts

### Discover

Input: provider capability, source URL, operator question, PIR, or source gap.

Output: candidate source reference with owner, access status, expected lane, and next check.
Discovery is not collection and cannot close a lane.

### Collect

Input: approved public/configured source.

Output: immutable source artifact reference plus observation metadata. A typed failure uses the
six-value source status vocabulary and never fabricates a checked result.

### Canonicalize

Input: provider-specific record and source artifact reference.

Output: versioned canonical sensor event. Raw fields are preserved by explicit mapping,
extension storage, or a hard validation error. Silent field loss is forbidden.

### Triage

Input: canonical events.

Output: deterministic priority, dedupe relation, defer/drop decision, and route to fast-only or
deep analysis. Every defer/drop decision is receipted. A quiet-anomaly budget protects rare lanes.

### Analyze

Input: bounded canonical event set and retrieval context.

Output: proposed Claims, Observations, Relationships, contradictions, missing context, and next
checks. Record model/version, prompt, budget, inputs, exclusions, and timestamps.

### Validate

Input: proposals plus source and transformation trace.

Output: validated candidate, quarantined candidate, or human-review requirement. Deterministic
validation controls schema, provenance, time, source independence, cue-only policy, and edge state.

### Persist Provenance

Input: canonical events and validated/proposed relationships.

Output: temporal provenance records with `valid_from`, `valid_to`, contradiction, retraction,
proposer, approver, and receipt references. Storage choice remains open.

### Select Thread State

Input: validated candidate packets and temporal state.

Output: append-only lineage plus strongest current state, retained/stale state, source gaps, and
RFI readiness. A newer weaker packet need not replace stronger current state.

### Present

Input: canonical read projections.

Output: one-shell current/retained/stale/unavailable views with claim-level trace. No visible
normal operator control mutates production authority.

### Review

Input: operator judgement and trace.

Output: acknowledgement, rejection, request for collection, or separately gated downstream
decision. Human review does not retroactively alter source artifacts or receipts.

## Retraction And Correction

Corrections append a new event and mark prior claim/relationship validity. They never rewrite
historical source artifacts or receipts. Retraction must propagate to retrieval, Threads, operator
views, and future analysis while preserving audit history.

## Freshness

Track source observation time, publication time, ingest time, canonicalization time, analysis
time, validation time, thread-selection time, and operator-review time separately. `current` is a
projection decision, not a synonym for recently generated.

## Replay

Given the same immutable source artifacts, contract versions, deterministic code, and fixed model
fixture, replay must reconstruct:

- canonical events;
- triage decisions;
- normalized fields;
- validator outcomes;
- relationship proposals and validation state;
- thread selection;
- claim/source trace.

Any nondeterministic model result remains a recorded proposal, not reconstructed fact.

## Compatibility

Each contract declares version, required fields, optional fields, unknown-field policy,
deprecation window, migration, and rollback. Adapter conformance must prove downstream consumers
remain unchanged when a provider is swapped.
