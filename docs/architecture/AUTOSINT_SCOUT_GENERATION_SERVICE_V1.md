# AUTOSINT ScoutGenerationService V1

- Status: Offline replay/test implementation
- Authority: Production Foundation V2.1 generation-service contract
- Version: 1.0
- Owner: AUTOSINT Control Plane
- Last reviewed: 2026-07-19
- Runtime truth: REPLAY_ONLY — no production queue, provider, or default switch is accepted
- Supersedes: None
- Superseded by: None
- Related: [Migration from Browser Runtime](AUTOSINT_MIGRATION_FROM_BROWSER_RUNTIME.md), [Control Plane V2](AUTOSINT_CONTROL_PLANE_V2.md), [Validation and Provenance V2](AUTOSINT_VALIDATION_AND_PROVENANCE_V2.md)

## Purpose

`ScoutGenerationService` is an API-neutral, durable-target interface for future
generation providers. The V1 foundation implements a deterministic in-memory
replay/test boundary and typed contracts. It does not replace, invoke, recover,
or modify the current browser External Scout lifecycle.

## Current Truth

The production default remains the scheduled browser prompt and matching
asynchronous harvester, followed by the existing normalizer, validators,
promotion/quarantine, Threads, and canonical proof reporter. V1 performs no
prompt, harvester, Chrome, AppleScript, launchd, inbox, staging, quarantine,
proof-history, or rotation action.

The local service implementation is replay/test only. It has no PostgreSQL
runtime proof, production worker, production provider, API route, or operator
control. `openai_responses` is disabled, has no model default, imports no SDK,
reads no key, and makes no API call.

## Target Interface

The service exposes:

- `submit_task(request, idempotency_key)`
- `get_task(task_id)`
- `cancel_task(task_id, reason, actor)`
- `stream_events(task_id, after_sequence)`
- `retrieve_result(task_id)`
- `replay_task(task_id, idempotency_key)`
- `health()`

Worker execution is an internal queue concern. The current implementation adds
`process_next()` only for deterministic local tests; it is not a production
worker or lifecycle scheduler.

## State And Idempotency Contract

```text
SUBMITTED -> VALIDATING -> QUEUED -> RUNNING
RUNNING -> RESULT_RECEIVED -> VALIDATING_RESULT -> SUCCEEDED
VALIDATING|VALIDATING_RESULT -> REJECTED_VALIDATION
QUEUED|RUNNING -> CANCEL_REQUESTED -> CANCELLED
RUNNING|VALIDATING_RESULT -> RETRY_WAIT -> QUEUED
RETRY_WAIT with exhausted attempts -> DEAD_LETTERED
active task past deadline -> TIMED_OUT
```

Idempotency uniqueness is `(provider_id, idempotency_key)`. The same key and
canonical request hash returns the existing task and appends no event. The same
key with a different hash returns `IDEMPOTENCY_CONFLICT`. Replay creates a new
task linked by `replay_of_task_id`; it never reopens or overwrites terminal
history.

Queue ordering is priority descending, creation time ascending, then task id.
The in-memory replay repository models this order. A PostgreSQL implementation
must claim work with `FOR UPDATE SKIP LOCKED` and a bounded lease.

## Event, Result, Retry, And Cancellation Rules

- Task state is mutable only through the validated state machine.
- Events and results are append-only.
- Every event has a per-task sequence and chained SHA-256 digest.
- Provider failures retain a bounded safe code/class only.
- Retry count, deadline, and attempt count are bounded.
- Dead-lettered work is not automatically replayed.
- Cancellation is cooperative. A result arriving after cancellation or timeout
  is discarded and audited; it cannot become a result.
- A successful task means a candidate result was processed. It does not mean
  validation/promotion by the production External Scout pipeline.

## Provider Boundary

| Provider | V1 state | Allowed behavior |
|---|---|---|
| `test_fixture` | Enabled | Fixed injected fixtures, no network or credentials |
| `browser_diagnostic` | Replay-only | Recorded artifacts only; no live browser, prompt, harvester, capture, or recovery |
| `openai_responses` | `enabled=false` | No SDK import, model default, key read, trace, or API call |

No provider can select system-contract identity, normalize, validate, promote,
quarantine, update Threads, advance proof, or mutate Evidence, cases, sources,
OSIR, apply/import, rotation, or commander-ready state.

## Validation And Privacy

Requests and results are bounded typed objects. They must remain
`candidate_only=true`, `promotion_performed=false`, and
`mutation_authority=none`. Payload size, provider, task type, timeout, attempt,
fixture mode, and forbidden context keys are validated. Credential, token,
password, cookie, session, browser-profile, Keychain, raw-Evidence, and private
conversation fields are rejected.

Telemetry includes counts, queue age, status, provider health, retries, and
safe hashed identifiers. It excludes request/result payloads, prompts, outputs,
credential values, and raw provider transcripts.

## Persistence Target

The accepted PostgreSQL target adds three isolated `public` tables in an
ordered follow-on migration:

- `scout_generation_tasks`
- append-only `scout_generation_events`
- one-to-one append-once `scout_generation_results`

They have no foreign key to current pending files, inbox, staging, quarantine,
Threads, cases, Evidence, sources, OSIR, proof, or rotation. The current pending
and generation-progress files remain browser-runtime authority until migration
acceptance. V1 does not backfill or dual-write them.

## Acceptance

Production acceptance requires PostgreSQL persistence and restart proof;
idempotency, lease, retry, cancellation, timeout, dead-letter, and replay tests;
provider failure and privacy tests; API/UI degraded-state tests; unchanged
normalizer/validator/promotion/Thread/proof semantics; authentication/RBAC for
any future control; staging soak; operator UAT; and explicit go/no-go approval.

Until those gates pass, the service remains replay/test only, the OpenAI
provider remains disabled, and the browser production default is unchanged.

## Rollback

Disable replay/test workers, stop leasing new tasks, terminalize or expose
in-flight state honestly, and preserve append-only events/results. Rollback
does not retry the current browser lifecycle, delete receipts, reopen terminal
tasks, reuse mismatched output, or change any production default.
