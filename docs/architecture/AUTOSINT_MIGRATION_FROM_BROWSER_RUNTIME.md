# AUTOSINT Migration from Browser Runtime

- Status: Target migration plan
- Authority: Production Foundation V2.1 browser-runtime migration target
- Version: 1.0
- Owner: AUTOSINT Architecture and Operations
- Last reviewed: 2026-07-19
- Runtime truth: NO — no provider switch or browser-runtime migration is accepted
- Supersedes: None until acceptance
- Superseded by: None
- Related: [Production Architecture V2.1](AUTOSINT_PRODUCTION_ARCHITECTURE_V2_1.md), [Sensor and Collection Plane V2](AUTOSINT_SENSOR_AND_COLLECTION_PLANE_V2.md), [Security and Deployment V2](AUTOSINT_SECURITY_AND_DEPLOYMENT_V2.md)

## Purpose

This plan removes workstation/browser requirements from the future production
generation path without disrupting the current validated External Scout
runtime. Migration is incremental, replay-first, fail-closed, and reversible.

## Current Truth

The current production default remains:

```text
:00 scheduled browser prompt
  -> exact pending request and attempt binding
  -> :28 asynchronous browser harvester
  -> Scout Findings normalization
  -> deterministic validation and preservation
  -> quarantine or promotion
  -> Threads
  -> /external-scout/24-7 proof and health
```

Manual prompt, harvester, capture, recovery, browser inspection, or launchd
mutation is outside this architecture task. A matching pending request forbids
duplicate lifecycle action. Current proof requires natural receipt-backed
cycles and remains owned by the canonical same-source reporter.

## Target Design

The target generation interface is API-neutral and platform-independent:

```text
typed generation task
  -> durable idempotent queue
  -> allowlisted provider adapter
  -> typed generation events and result
  -> unchanged deterministic normalizer/validators
  -> unchanged promotion/Thread/proof authority
```

It provides `submit_task`, `get_task`, `cancel_task`, `stream_events`,
`retrieve_result`, `replay_task`, and `health` with versioned task, result, and
event contracts. Queue states, timeouts, retries, cancellation, dead-letter,
telemetry, and receipts are explicit.

The target path must not require a consumer ChatGPT browser, specific tab,
AppleScript, macOS GUI, unlocked laptop, workstation launchd, or consumer model
selection.

### Provider States

| Provider | State during V2.1 foundation | Production authority |
| --- | --- | --- |
| Current browser runtime | Enabled current default | Unchanged until final acceptance |
| `test_fixture` / deterministic replay | Enabled for tests and demo | None |
| `browser_diagnostic` | Existing bounded diagnostic semantics only | Never counts as natural proof by itself |
| `openai_responses` | `enabled=false` | No API call, no key read, no default selection |

Provider output remains candidate input. It cannot select system-contract
identity, validation policy, promotion, proof, or Thread-current authority.

### Migration Stages

#### Stage 0 — Baseline And Freeze

Inventory the current browser lifecycle, identities, receipts, timeouts,
validation counters, proof inputs, and failure modes. Establish regression
fixtures. Do not change the default.

#### Stage 1 — Contract And Deterministic Replay

Implement the API-neutral task/result/event contracts and replay provider.
Feed only sanitized fixed fixtures through the same normalizer, validators, and
projections. Prove idempotency, cancellation, timeout, restart, and dead-letter
behavior. The current browser runtime remains untouched.

#### Stage 2 — Offline Parity

Replay previously sanitized accepted and rejected fixture cases through both
contract boundaries. Compare normalized payload hashes, all validation
counters, preservation, quarantine/promotion eligibility, Thread projections,
and proof inputs. This stage submits no live duplicate generation.

#### Stage 3 — Separately Approved Non-Production Provider

Only a future explicit task may enable `openai_responses` in isolated staging.
That task must use official provider documentation, approved credentials and
egress, sanitized inputs, bounded cost/latency, tracing redaction, and mocks
before any real call. It does not change the production default or current
proof streak.

#### Stage 4 — Staging Soak And Operator UAT

Prove queue reliability, provider failures, output parity, validator behavior,
degraded states, privacy, audit, and rollback over an approved staging soak.
Maintain one operator shell and one canonical proof source. Do not combine
provider snapshots into one apparent cycle.

#### Stage 5 — Explicit Default Switch

A default switch requires all production acceptance gates and a recorded human
go/no-go decision. Change one provider binding at a controlled boundary; do not
run browser and API providers as competing production producers for the same
request. Existing pending work is terminalized under its original provider.

#### Stage 6 — Browser Diagnostic Retirement

Only after sustained accepted operation may the browser path move from current
default to bounded diagnostic/fallback status. Retain replay compatibility and
historical receipts. Removal requires separate lifecycle/reference proof.

### Proof And Identity Continuity

The existing machine-owned `expected_contract_* -> bound_contract_* ->
validation_contract_*` chain remains authoritative. Model/provider-reported
identity stays diagnostic only. The canonical proof builder is extended, if
required and accepted, to understand the new provider receipts; no second
proof page or calculation is created.

Natural-cycle eligibility remains provider- and receipt-bound. Replay,
diagnostic capture, manual recovery, and staging calls never advance production
proof.

### Human Approval And Privacy

Enabling staging, selecting a production provider, changing the default, and
retiring browser production each require separate authenticated human
decisions and audit receipts. No migration stage reads credential values,
browser sessions/storage/profiles, cookies, Keychain data, private conversation
ids, raw Evidence bodies, or unrelated runtime artifacts.

No PIR or Agent event may trigger generation directly without an accepted
Control Plane task, allowlisted policy, and human approval when required. Such
events retain `mutation_authority=none` over canonical state.

## Acceptance

The browser production default may change only when all of these are proven:

1. deterministic task/result/event contracts and replay tests;
2. exact request/attempt identity, idempotency, pending, cancellation, timeout,
   retry, and dead-letter semantics;
3. normalization, structural, semantic, preservation, freshness, quarantine,
   promotion, Thread, and proof parity;
4. no duplicate generation or mixed-provider current state;
5. platform-independent deployment and degraded-mode behavior;
6. authentication/RBAC, privacy, egress, audit, cost, and incident controls;
7. current External Scout regression, staging soak, and operator UAT;
8. explicit human go/no-go and tested rollback.

Until every gate passes, `Runtime truth` is `NO`, the OpenAI provider stays
disabled, and the browser runtime remains the production default.

## Rollback

Before a default switch, rollback disables the new provider/worker and leaves
the browser path unchanged. After an accepted switch, rollback stops new queue
leases, terminalizes in-flight work under its original provider, restores the
last accepted provider binding, and verifies canonical proof/Thread reads.
Rollback never duplicates a pending prompt, manually harvests, rewrites proof,
reuses mismatched output, deletes receipts, or changes production data.
