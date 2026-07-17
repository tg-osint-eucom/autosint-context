# AUTOSINT Operating Model Current

- Status: Current
- Authority: Canonical architecture
- Owner: AUTOSINT Architecture
- Last reviewed: 2026-07-16
- Runtime truth: No; live state requires current receipts and reports
- Supersedes: Historical multi-shell and direct-packet operating summaries
- Superseded by: None
- Related: [System Contract](status/AUTOSINT_SYSTEM_CONTRACT_CURRENT.md), [Primary Workflow](AUTOSINT_PRIMARY_WORKFLOW.md), [External Scout Runbook](AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md)

## Purpose

AUTOSINT is a local-first operator review system. It accepts public candidate
input, validates and organizes it, preserves provenance and degraded states,
and exposes one read-only operating picture. Candidate material remains outside
Evidence, OSIR, apply/import, and commander-ready authority.

Cross-cutting invariants are machine-readable in
`config/autosint_system_contract.yml`. Detailed sensor and workstream truth
remains in the referenced registries rather than being duplicated here.

## One Operator Shell

The current operator path is:

```text
Mission Control
-> External Scout
-> Threads
-> RFI
-> future controlled approval
```

Primary routes:

- `/mission-control`: workflow launch page.
- `/external-scout/24-7`: single pinned External Scout proof and health page.
- `/external-scout`: validated packet inbox/support view.
- `/external-scout/threads`: durable thread-current and Live Case Board.
- `/external-scout/24-7/proof-data`: styled same-source proof view.
- `/rfi`: theater/workspace overview.
- `/rfi/{workspace}`: read-only selected-thread/case preview.

The machine-readable RFI routes are `/api/v1/rfi` and
`/api/v1/rfi/{workspace}`. There is no compatibility route or second dashboard
for the superseded product vocabulary.

## External Scout Producer And Consumer

The configured Packet chat is the producer workspace. ChatGPT produces Scout
Findings under the exact pending request and generation attempt. AUTOSINT then
normalizes the findings into strict candidate packets.

- Producer mode: `scout_findings_normalized`.
- Direct strict packets: fallback/replay only.
- Primary transport: `inline_fenced_json`.
- Fallback transport: `downloadable_json_attachment` only when inline cannot
  be produced.
- Both full payloads in one response: forbidden.
- Natural cases: 1-3 by default, absolute maximum 5.
- Explicit bounded recovery: exactly 1 case.

The scheduled local prompt trigger and scheduled async harvester are runtime
actors under one contract. ChatGPT Scheduled Tasks are not a separate producer
authority. Runtime load state belongs in current launchd/receipt reports, not
this architecture document.

## Request And Attempt Lifecycle

Every cycle persists:

- system contract version and SHA;
- root trigger request id;
- generation attempt id and number;
- producer and requested transport;
- case policy and model policy fields.

Page-global busy without exact attempt ownership is ambiguous. It cannot
authorize a second submit, clear pending state, create a replacement root, or
prove useful progress. The harvester fails closed on stale, mismatched,
wrong-attempt, wrong-contract, or expired output.

## Validation And Promotion

The candidate path is:

```text
Scout Findings
-> staging
-> deterministic normalization
-> structural validation
-> semantic validation
-> preservation validation
-> freshness/newer-than-inbox gate
-> inbox promotion or quarantine/skip
-> thread-current selection
```

Promotion requires the three core error counters to be zero:

- `structural_validation_error_count`
- `semantic_validation_error_count`
- `preservation_error_count`

The theater contract also exposes fail-closed diagnostics, all of which must
be zero:

- `global_coverage_validation_error_count`
- `theater_semantic_error_count`
- `cross_theater_duplicate_count`

A structurally generated `Not checked` row is honest accounting, not proof of
collection. Invalid output never updates active state.

## Sensor And Source Contract

The global sensor policy distinguishes 13 canonical categories from 19
operational lanes. Every required lane must be explicitly accounted for using
the versioned source-status vocabulary. This includes:

- three prediction-market rows: Polymarket, Kalshi, and Manifold / Other
  Prediction Markets;
- eight market/finance rows including `insurance_freight_rates`;
- seven configured theater rows. Row presence is structural accounting; it is
  not equivalent to seven theaters checked.

Coverage truth is multi-dimensional:

- `coverage_status`
- `follow_up_statuses`
- `blocked_source_count`
- `candidate_source_count`
- `stale_source_count`
- `checked_source_count`

A valid checked source is not downgraded because another source is blocked,
candidate-only, or stale. Those follow-ups remain visible WARN items.

Markets, finance, prediction markets, crypto, social OSINT, and public comments
are cue-only. They cannot independently prove attribution, causality, intent,
closure, Evidence, OSIR, case linkage, or commander-ready status.

## Threads And Live Case Board

`/external-scout/threads` owns durable thread-current state. Current, retained,
stale, archived, unavailable, and no-data states remain distinct. A retained
thread can preserve continuity but cannot masquerade as a fresh packet.

Thread selection prefers the newest validator-clean current packet while
preserving historical lineage and source gaps. RFI consumes thread-current
state first and validated packet fallback only when thread-current is
unavailable.

## RFI

RFI renders a read-only operator preview.

- `/rfi` owns theater/workspace organization.
- `/rfi/{workspace}` owns selected case/thread preview.
- RFI is analyst-review-only and candidate-input-only.
- RFI does not create Evidence, mutate cases or sources, open OSIR, perform
  apply/import, or set commander-ready state.

## Proof And Health

The canonical proof reporter requires three consecutive eligible natural
prompt-to-async-harvester cycles. Each cycle separately proves prompt
submission, user-turn persistence, response start, exact output identity,
normalization, structural/semantic/preservation success, promotion, board
freshness, active threads, and no RED health.

Runtime proof, global theater coverage, and deep-dive rotation are separate
truth dimensions. The proof target remains three consecutive eligible natural
cycles. Coverage independently reports `COMPLETE`, `INCOMPLETE`, `STALE`, or
`UNKNOWN`; rotation independently reports `CURRENT`, `DUE`, `OVERDUE`, or
`UNINITIALIZED`. `PROVEN` never implies seven theaters were checked.

Manual recovery and direct capture never advance proof. A known operator pause
explains interruption but invalidates current proof until natural cycles
rebuild it. Current proof count, health, launchd state, packet timestamp, and
thread counts belong in current reports and receipts, not this document.

## Contract Guard And Degraded Mode

The deterministic Contract Guard runs at API startup and before scheduled
prompt/harvester browser action. It also participates in proof, health,
Operator Terminal, release validation, and context-mirror preflight.

- WARN is visible and does not block normal runtime.
- RED blocks scheduled actors before browser action.
- AUTOSINT.app and read-only APIs remain available under RED with
  `CONTRACT_CONFLICT_RED`.

The Operator Terminal is read-only. It displays contract load, pass, warning,
manual-setting verification, and conflict events. It has no command input,
reset control, or automatic fixer.

## Capability Truth

Capabilities use the evidence-qualified vocabulary defined by the system
contract. Code existence alone does not prove app integration or operational
proof. `APP_INTEGRATED` requires a registered route, navigation path, rendered
state, canonical source, focused tests, and honest current/no-data/degraded
states. `OPERATIONALLY_PROVEN` additionally requires receipt-backed runtime
evidence.

Current bounded classifications include:

- External Scout and RFI operator routes: read-only app surfaces with focused
  route tests; current runtime still depends on receipts.
- PIR Hunter: advisory/read support; it does not redefine External Scout proof.
- Agent Exchange: storage/read provenance and gated writes; no autonomous
  recipient/delivery claim without transport evidence.
- Operator Hub: candidate discovery/status support, not Evidence.
- Operator Scheduler: backend/write-capable and execution-gated; no normal UI
  execution path.
- `/moltbook`, `/dagrbook`, and `/control-plane`: `LEGACY_REMOVED` routes.

## Model Policy

The required ChatGPT Project label is `GPT-5.6 Sol Pro`, with selection status
`OPERATOR_CONFIRMED`. Account-setting machine verification is not performed,
cycle attribution requires an approved receipt, and no API model id is inferred.
Model evaluation remains separate from runtime recovery and production API
migration.

## Proposed Architecture Boundary

The Lattice-inspired reference architecture, target data lifecycle, trust
model, latency SLO, and orchestration roadmap are proposals with
`Runtime truth: No`. They do not prove current implementation.

Canonical event and provenance contracts come before any future GraphRAG,
graph database, vector database, new event bus, or autonomous agent transport.
Those remain `EVALUATE_LATER` and are outside this operating model.

## Safety Boundary

AUTOSINT review surfaces are read-only by default. No normal operator path in
this model authorizes:

- DB or raw Evidence mutation;
- case-link or source-config mutation;
- OSIR bypass or apply/import;
- commander-ready promotion;
- browser-private-state, credential, token, or `.env` value access;
- autonomous PIR/Agent writes or Operator Scheduler execution.

`commander_ready=false` and `mutation_performed=false` are preserved throughout
External Scout and RFI candidate handling.
