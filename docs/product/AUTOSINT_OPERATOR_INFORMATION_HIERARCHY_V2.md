# AUTOSINT Operator Information Hierarchy V2

- Status: Implemented preview contract; runtime acceptance pending
- Authority: Production Foundation V2.1 product hierarchy
- Version: 2.1
- Owner: AUTOSINT Operator Experience
- Last reviewed: 2026-07-19
- Supersedes: No current route until preview acceptance
- Superseded by: None
- Runtime truth: PARTIAL — tracked default-off preview only; current production routes remain authoritative

## Decision

AUTOSINT keeps one application shell and one External Scout proof source. The
V2 preview reorganizes existing read APIs into seven operator questions without
copying their builders or changing current state:

1. `MISSION`: what requires attention and human review?
2. `WATCH`: what is current, stale, blocked, or unproven in the watch loop?
3. `CASES`: which Thread-current cases and lineage are active?
4. `PIR`: which advisory questions have validated coverage, contradictions, and gaps?
5. `AGENTS`: what bounded task, handoff, critique, guardrail, and result events occurred?
6. `RFI`: what is safe for analyst preview and what remains limited?
7. `SYSTEM`: what service, database, collection, integration, and validation blocker exists?

## Truth Order

Every card shows the data state, source API, source timestamp when supplied,
limitations, and safe next action before audit detail. `WATCH` reads
`/api/v1/external-scout/24-7-proof`; it never recomputes proof. `CASES` reads
the existing Threads API. PIR and Agents read their dedicated V2 projections.
An unavailable endpoint renders `DEGRADED`, `DB_SERVICE_UNAVAILABLE`,
`GATED_DISABLED`, or `ERROR`; legacy data is not substituted.

## Main Versus Audit

The main hierarchy shows outcomes, changes, validation, gaps, ownership, and
next checks. Raw JSON, identifiers, URL lists, hashes, counters, and provenance
remain inside a collapsed Audit disclosure. The preview uses text-only DOM
rendering for payload data, so response values are not interpreted as HTML.

## Controlled Briefing Mode

`operator_briefing_mode_enabled=false` adds no route while the parent UI flag
is off. When both flags are explicitly enabled for an isolated loopback
preview, the same shell presents a sanitized `FIXTURE` mission, curated case
briefings, all 19 canonical operational sensor lanes, a fixture PIR board, the
existing deterministic Agent event replay, and a same-bundle RFI summary.

The operator layer remains `MISSION | WATCH | CASES | PIR | AGENTS | RFI`.
`SYSTEM` is secondary and starts collapsed. Every briefing page permanently
states that fixture/replay/current/retained/stale sources are distinct and
that no exhaustive coverage or operational authority is claimed.

The hierarchy is fail-closed:

- `Not checked` registry rows are not collection;
- cue-only rows remain cue-only;
- candidate rows remain unimported;
- fixture freshness is not live currentness;
- Agent events with no typed case link render `NO_TYPED_CASE_LINK`;
- model or Agent text alone cannot answer a PIR;
- no private path, receipt name, unredacted Evidence content, full hash, or write control
  belongs in the default briefing view.

## Control Boundary

The preview has links and read-only filters only. It contains no form, command
box, prompt, capture, recovery, scheduler, agent-start, Evidence, case-link,
source-config, OSIR, apply/import, reset, or commander-ready control. The
tracked flag is `new_operator_ui_enabled=false`. Enabling it permits only a
loopback preview route; it does not enable any write gate.

## Accessibility And Layout

The shell uses semantic landmarks, a skip link, visible focus, keyboard-safe
links and disclosures, high-contrast tokens, reduced-motion support, and a
single-column mobile layout. Long values wrap instead of widening the page.
Every data state has text in addition to color.

## Acceptance Boundary

This hierarchy becomes the normal operator shell only after feature-flag-off
regression, route/API contract checks, desktop/mobile/keyboard/contrast QA,
state coverage, operator UAT, and current External Scout regression checks pass.
Until then the current routes and proof source remain unchanged.
