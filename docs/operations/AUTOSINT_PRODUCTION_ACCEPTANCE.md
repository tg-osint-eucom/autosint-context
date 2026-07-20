# AUTOSINT Production Acceptance

- Status: Current gate policy
- Authority: `PRODUCTION_ACCEPTANCE_MATRIX.csv` and the V2.1 program goal
- Version: 2.1
- Owner: AUTOSINT Release Authority
- Last reviewed: 2026-07-20
- Supersedes: Ad hoc readiness conclusions
- Superseded by: None
- Runtime truth: `HOLD` — a production-grade foundation for a controlled SOCOM pilot is being implemented, but pilot acceptance has not passed

## Decision

AUTOSINT Production Foundation V2.1 is not a pilot release authorization. The
release decision is `HOLD` until every required gate in
`PRODUCTION_ACCEPTANCE_MATRIX.csv` is `PASS`. `PASS_WITH_SCOPE` records useful
bounded implementation evidence but does not close a production gate.

Tests, HTTP 200, route registration, fixture replay, a screenshot, or an old
receipt cannot independently satisfy a runtime gate. Current timestamps and
same-source evidence are mandatory. Current External Scout proof, theater
coverage, database readiness, PIR/Agent readiness, and pilot readiness remain
separate truth axes.

## Gate vocabulary

- `PASS`: the exact gate has current, reproducible acceptance evidence.
- `PASS_WITH_SCOPE`: a narrower offline/read-only/replay contract passed; the
  full production gate remains open.
- `BLOCKED`: a named current blocker prevents the required validation.
- `NOT_OBTAINED`: the required exercise or approval has not occurred.
- `HOLD`: aggregate release decision; pilot operation is not authorized.

## Required decision rule

`PILOT_GO=PASS` only when all preceding required gates are `PASS`, the evidence
timestamps are still valid, the staged artifact matches the reviewed commit,
the current External Scout default has not regressed, and the operator signs
the go/no-go checklist. Any `BLOCKED`, `NOT_OBTAINED`, or `PASS_WITH_SCOPE`
forces `PILOT_GO=HOLD`.

## Current blockers

- The operator decision `PRESERVE_UNTOUCHED_EXISTING_PGDATA` cleared only the
  isolated local development/test PostgreSQL gate. The unknown host candidate
  remains untouched and unused; production database target approval is still
  absent.
- Production database target approval is absent.
- Authentication and PIR-specific RBAC are not implemented/accepted; PIR CRUD
  remains default-off.
- Source-adapter conformance, model replay, human operator UAT, staging soak,
  production backup/restore acceptance, and incident-response rehearsal are
  not complete. The isolated synthetic backup/restore result does not close the
  production gate.
- Current deterministic Agent replay and MCP read-only handshake do not grant
  agent mutation, model-provider, or production orchestration authority.

The independent rendered engineering harness may record
`CODEX_RENDERED_UAT_PASS` after its exact browser and screenshot gates pass.
That result does not claim `OPERATOR_UAT_PASSED`, enable UI V2 by default, or
change the aggregate pilot decision from `HOLD`.

Likewise, applied PIR tables and a synthetic schema-persistence smoke do not
prove a PostgreSQL-backed `PirAdvisoryRepository` exists in the canonical app;
its current service remains deterministic replay. The isolated Agent
event-store persistence/reconnect/idempotency smoke proves bounded append-only
SQL behavior only, not production/OpenAI mode or autonomous authority.

A passing canonical release-surface validation together with
`CODEX_RENDERED_UAT_PASS` may support the pre-push engineering verdict
`READY_FOR_FINAL_PUSH_APPROVAL`. That verdict is not `PILOT_GO`, production
release, or authorization to push without the separate exact-series approval.

## Evidence requirements

Every passing row records the commit, command or receipt, generated timestamp,
scope, expected result, observed result, and rollback path. Evidence must avoid
secrets, raw Evidence bodies, browser/session state, private conversation ids,
and database dumps. Runtime evidence is ignored and never staged.

## Safety boundary

Acceptance does not authorize Evidence, case-link, source, OSIR, apply/import,
commander-ready, proof, rotation, collector, scheduler, browser, launchd, or
model-default mutation. Those actions require their own explicit authority.
