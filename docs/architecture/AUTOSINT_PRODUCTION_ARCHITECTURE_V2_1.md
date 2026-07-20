# AUTOSINT Production Architecture V2.1

- Status: Target architecture
- Authority: Production Foundation V2.1 target design
- Version: 2.1
- Owner: AUTOSINT Architecture
- Last reviewed: 2026-07-19
- Runtime truth: NO — this target is not implemented or accepted
- Supersedes: None until the production acceptance gates pass
- Superseded by: None
- Related: [Current Operating Model](../AUTOSINT_OPERATING_MODEL_CURRENT.md), [System Contract](../status/AUTOSINT_SYSTEM_CONTRACT_CURRENT.md), [Control Plane V2](AUTOSINT_CONTROL_PLANE_V2.md), [Data Plane V2](AUTOSINT_DATA_PLANE_V2.md)

## Purpose

This document defines the target production-grade foundation for a controlled
SOCOM pilot. It is an architecture contract, not a live-state report, an ATO,
SOCOM production authorization, or a claim of commander-ready authority.

## Current Truth

Current implementation and runtime truth remain owned by tracked code, current
config, tests, receipts, health reports, and the canonical proof reporter.

- The current production input is the browser-mediated External Scout
  Scout Findings path.
- `/external-scout/24-7` and
  `/api/v1/external-scout/24-7-proof` remain the single External Scout proof
  surface and same-source machine authority.
- `/external-scout/threads` remains durable thread-current case memory.
- PIR is currently advisory/read support; a dedicated PIR workflow is not yet
  accepted.
- Agent storage and gated writes do not prove recipient/delivery transport or
  bounded collaboration.
- PostgreSQL ownership is split between unqualified `public` objects and
  legacy `idos.*` consumers; the target decision below is not yet migrated.
- Current runtime may depend on a consumer ChatGPT browser, macOS UI automation,
  and workstation scheduling. That path remains operational until migration
  acceptance; this document does not switch it.

## Target Design

```text
Operator App
  -> Mission / PIR Control Plane
  -> Typed Task Queue
  -> Manager-Controlled Agent Runtime
  -> Sensor / Adapter Plane
  -> Validation and Provenance
  -> PostgreSQL Data Plane
  -> Canonical Read APIs
  -> Human Approval Boundary
```

Cross-cutting planes provide authentication and authorization, privacy,
observability, immutable audit, configuration, idempotency, degraded-state
handling, and rollback.

### Binding Decisions

| Decision | V2.1 target |
| --- | --- |
| Operator application | One shell inside the existing AUTOSINT server boundary. |
| External Scout truth | One canonical proof builder and same-source API; no second Live Board or proof source. |
| Current browser runtime | Preserved as production default until every migration acceptance gate passes. |
| Database schema | `public` is the canonical V2.1 application schema. No new canonical tables are created in `idos`. |
| Legacy `idos.*` | Temporary read-only compatibility views/adapters only, with measured parity and an explicit retirement gate. |
| PIR authority | Dedicated advisory domain only; no Evidence, case, source, packet, Thread, OSIR, apply/import, proof, or commander-ready mutation. |
| Agent authority | Dedicated task/run/event store only; every role has `mutation_authority=none`. |
| Agent coordination | Manager-controlled typed tasks and allowlisted handoffs, never uncontrolled peer chat. |
| Model provider | Deterministic replay/local test first. The OpenAI adapter remains `enabled=false`; no key read or API call is authorized. |
| Human authority | High-impact actions remain outside candidate projections and require authenticated, authorized, explicit human approval with an audit event. |
| Deployment target | Platform-independent services; no required consumer ChatGPT tab, AppleScript, macOS GUI, unlocked laptop, single-workstation launchd, or consumer model selection. |

### Authority Boundaries

| Plane | May own | Must not own |
| --- | --- | --- |
| Control Plane | Missions, PIR orchestration intent, typed task lifecycle, approvals requested | Evidence, case truth, source configuration, proof history |
| Agent Runtime | Bounded runs, tasks, handoffs, critiques, candidate findings | Canonical packet/Thread/case mutations or autonomous approval |
| Sensor / Adapter Plane | Public/configured collection attempts and typed results | Coverage claims without validated evidence; downstream authority |
| Validation / Provenance | Deterministic verdicts, transformations, lineage, quarantine | Source fabrication or model-selected authority |
| Data Plane | Canonical persistence, read models, receipts, event stores | Silent cross-schema duplication or history rewrite |
| Operator UI | Read projections and explicitly gated review actions | Hidden writes, parallel truth, autonomous start controls |

### Human Approval Boundary

PIR advisory edits, agent review decisions, and future downstream actions are
separate authority classes. A permitted write requires an authenticated
operator, role permission, explicit request, exact scope, policy decision,
idempotency key, audit receipt, and `mutation_performed` result. Evidence,
case-link, source-config, OSIR, apply/import, proof-history, rotation, and
commander-ready authority remain closed in V2.1.

### Failure And Degraded Operation

Each projection must distinguish current, retained, stale, blocked,
candidate-only, not-checked, unavailable, unknown, and gated-disabled states.
A failed provider, model, database, queue, or UI does not authorize fallback
writes or a GREEN/PROVEN claim. Last-known-good data remains explicitly stale.

### Privacy And Security

Canonical services process only allowlisted inputs and minimum necessary
context. Cookies, sessions, browser storage, Chrome profiles, Keychain values,
credential values, `.env` values, raw Evidence bodies, private conversation
identifiers, and production database contents are excluded from agent/model
contexts, logs, traces, screenshots, handoffs, and public mirrors.

## Acceptance

`Runtime truth` may change from `NO` only after repository evidence proves all
applicable production-acceptance gates, including:

1. canonical PostgreSQL migrations and `public`/`idos` compatibility parity;
2. deterministic PIR read model with no canonical-state mutation;
3. deterministic agent replay, event-store, handoff, and guardrail tests;
4. one-shell UI consuming canonical APIs with feature flag off by default;
5. canonical MCP read-only handshake and all write gates off;
6. authentication/RBAC for every enabled operator write;
7. backup/restore, degraded-mode, privacy, and rollback tests;
8. current External Scout regression suite and unchanged proof authority;
9. staging soak and explicit operator go/no-go decision.

Until then the architecture status is target-only, production remains on the
current browser path, and no component may claim `PROVEN`, `APP_INTEGRATED`, or
production readiness from this document.

## Rollback

Every target component is introduced behind a default-off feature flag or an
isolated replay/test mode. Rollback disables the new route/provider/worker,
stops new advisory/event-store writes, preserves append-only audit records,
and returns reads to the prior canonical projection. Rollback never rewrites
proof history, deletes source artifacts, or promotes retained state to current.
