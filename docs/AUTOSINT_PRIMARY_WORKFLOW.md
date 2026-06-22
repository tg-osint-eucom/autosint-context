# AUTOSINT Primary Workflow

This document is the tracked source of truth for the current AUTOSINT operator path.

```text
Mission Control -> External Scout -> TSOC/HAVOC -> HAVOC/RFI -> future controlled approval
```

## Primary Pages

| Route | Role | Primary Question | Must Not Do |
| --- | --- | --- | --- |
| `/mission-control` | Primary launch page | Where should the operator start? | No writes, imports, OSIR bypass, or commander-ready promotion. |
| `/external-scout` | Primary external packet review | What fresh external candidate packets are active? | No Evidence or case-link creation; latest active capture only by default. |
| `/external-scout/{packet_id}` | Packet detail | What does one candidate packet say and what are its audit details? | No promotion/apply controls. |
| `/tsoc-havoc` | Theater/workspace organization | Which TSOC/workspace owns the topic and what is missing? | No case creation, source mutation, or OSIR bypass. |
| `/havoc-rfi/SOCCENT` | Human-readable package preview | What would the current SOCCENT HAVOC/RFI response package say? | Preview only; not commander-ready or OSIR export. |

## Supporting And Audit Pages

| Route | Role |
| --- | --- |
| `/case-genesis` | Supporting dry-run candidate formation and historical candidate review. |
| `/canonical-cases` | Supporting canonical case index and provenance entrypoint. |
| `/api/v1/cases/{case_id}/evidence-passport` | Evidence lineage and source traceability. |
| `/api/v1/cases/{case_id}/osir` | OSIR policy preview and blocker explanation. |
| `/api/v1/cases/{case_id}/audit-bundle` | Case audit bundle. |
| `/api/v1/pirs`, `/api/v1/pir-observations`, `/api/v1/overwatch` | PIR Hunter and Overwatch exception support. |
| `/api/v1/agent-feed`, `/api/v1/agent-threads/{thread_id}`, `/api/v1/agent-roster` | Agent Exchange audit/provenance and case-assist support. |
| `/api/v1/operator-hub/*` | Source-gap and discovery support. |

## Removed Legacy Browser Routes

These routes are not part of the current primary workflow:

- `/dagrbook`
- `/moltbook`
- `/control-plane`

DAGRBook assets and helpers may remain in the repo for future frontend-thread work, but they should not return to primary navigation without a separate approved design.

## Workflow Rules

- External Scout is the preferred external information-gathering input layer.
- AUTOSINT validates, normalizes, deduplicates, maps, previews, and gates.
- HAVOC/RFI should lead with validated External Scout operator fields when a suitable packet exists.
- Canonical cases, Case Genesis, source coverage, evidence passports, PIR, OSIR, and agent records are supporting/audit layers.
- ChatGPT output is not Evidence.
- Market, prediction-market, crypto, public-comment, and social reaction rows are cue-only unless later corroborated under existing AUTOSINT policy.
- Future import/apply must be explicit, receipt-backed, and preserve `commander_ready=false` unless OSIR policy allows otherwise.

## Next Architecture Milestones

1. Keep External Scout card/detail views operator-first and audit metadata collapsed.
2. Enable hourly local capture only after repeated dry-run and real capture validation.
3. Add External Scout Case Threads so repeated captures append to stable topic threads.
4. Integrate PIR Hunter as a priority-question / exception layer over External Scout threads and TSOC/HAVOC workspaces.
5. Simplify Source Library and hide audit-only coverage surfaces from the primary path.
6. Design a controlled apply/import path as a separate approval-gated workflow.
