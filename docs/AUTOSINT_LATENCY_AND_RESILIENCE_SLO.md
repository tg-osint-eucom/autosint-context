# AUTOSINT Latency And Resilience SLO

- Status: Proposed
- Authority: Reliability design proposal
- Version: 1.0
- Owner: AUTOSINT Reliability
- Last reviewed: 2026-07-15
- Runtime truth: No; thresholds require baseline and approval
- Supersedes: None
- Superseded by: None
- Related: [Reference Architecture](AUTOSINT_LATTICE_INSPIRED_REFERENCE_ARCHITECTURE.md), [Architecture Audit Question Bank](AUTOSINT_ARCHITECTURE_AUDIT_QUESTION_BANK.md), [External Scout Runbook](AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md)

## Objective

Measure time to useful operator value by mission and sensor tier while preserving accuracy,
provenance, and degraded operation. A universal ten-second SLO is not appropriate for every OSINT
workflow.

## Latency Events

| Metric | Start | End |
|---|---|---|
| `T_first_cue` | source observation or poll start | first bounded cue available |
| `T_first_useful_alert` | source observation or poll start | first operator-meaningful validated alert |
| `T_first_correlated_view` | first cue | first multi-source/thread-correlated projection |
| `T_first_operator_review` | first useful alert | operator acknowledgement or review |
| `T_full_assessment` | source observation or poll start | bounded complete assessment with gaps and contradictions |

Record p50, p95, p99, timeout rate, defer rate, queue time, processing time, provider wait,
model wait, validation time, UI publication time, and cost. Never collapse missing data into a zero
duration.

## Mission Tiers

### Tier 0 - Local Deterministic Safety

Examples: duplicate suppression, schema rejection, identity mismatch, stale detection, cue-only
gate. Target: synchronous or near-synchronous local execution. Must work without a frontier model.

### Tier 1 - Rapid Cue

Examples: high-priority official advisory, critical movement anomaly, source outage. Establish
thresholds only after baseline. The first cue may be partial but must state gaps and source status.

### Tier 2 - Correlated Operator View

Examples: thread update, multi-lane source comparison, initial PIR relevance. Optimize for a useful
validated view, not maximum narrative completeness.

### Tier 3 - Deep Assessment

Examples: multilingual synthesis, market/ship/insurance context, contradiction analysis. Longer
latency is acceptable when the queue, progress, budget, and missing lanes remain visible.

### Tier 4 - Replay / Audit

Examples: full provenance reconstruction, 100x replay, evaluation, export. Throughput,
reproducibility, and completeness take priority over interactive latency.

## Error Budget Policy

An SLO success requires valid and correctly labeled output. A fast invalid, stale, mismatched, or
untraceable result is a failure. Recovery-assisted cycles are recorded separately from natural
production evidence.

## Degraded Modes

| Failed dependency | Required surviving behavior |
|---|---|
| One adapter/provider | Other lanes continue; failed lane is typed and visible. |
| Frontier model | Deterministic collection, triage, validation, retained state, and UI remain usable. |
| Browser/ChatGPT upstream | Existing AUTOSINT read projections remain available with stale/unavailable labels; no duplicate prompt. |
| Harvester | Pending state and exact blocker remain visible; no promotion. |
| Database | Non-DB External Scout proof/read artifacts remain available where architecture permits; DB-backed views show explicit unavailable state. |
| Network | Local last-known-good state remains read-only; new collection is blocked/stale and queued only under an approved store-and-forward contract. |
| Proof reporter | No PROVEN/GREEN claim; supporting pages must not invent proof. |
| AUTOSINT viewer | Machine-readable same-source reports remain available; UI-host failure is explicit. |

## Retry And Circuit Breaker Rules

- retries are bounded by dependency and mission tier;
- exponential backoff includes jitter where safe;
- idempotency prevents duplicate prompts, tasks, collections, and promotions;
- a circuit breaker opens after a defined failure budget;
- retries cannot bypass identity, validation, freshness, or mutation gates;
- operator recovery is labeled and excluded from natural proof;
- pending intent survives restart only through an explicit persistence contract.

## 100x Evidence Gate

No 100x-scale claim is allowed until synthetic replay measures:

- event rate, queue depth, lag, and partition skew;
- dedupe, drop, and defer rates;
- quiet-anomaly recall;
- storage and artifact growth;
- provider/API budgets and throttling;
- model concurrency, timeout, and cost;
- UI/proof/thread publication lag;
- restart, replay, and reconciliation.

Point-in-time architecture scores belong in dated audit/scorecard artifacts,
not this durable target SLO. Until a dated replay report proves the gate, the
100x claim remains `NOT_PROVEN`.

## Availability And Recovery

Define target availability and recovery objectives only after the dependency map and baseline.
Required measurements include detection time, time to explicit degraded state, recovery time,
replay window, unprocessed intent count, duplicate count, and data-loss window.

## Validation Before Acceptance

1. deterministic timestamp contract;
2. latency instrumentation tests;
3. per-tier baseline;
4. fault matrix and chaos tests;
5. store-and-forward/reconciliation tests where approved;
6. operator recognition study for degraded states;
7. privacy and mutation-boundary verification.
