# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from private AUTOSINT source-of-truth docs and safe local status, without copying runtime artifacts or private browser state.

## Source

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source branch: `main`
- Source HEAD: `76ff62482f6abe025e48a672bad8cc38d97c0086`
- Generated at: `2026-07-20T22:03:38Z`

## Primary Workflow

`Mission Control -> External Scout -> Threads -> RFI -> future controlled approval`

## Primary Route Roles

- `/mission-control`: operator launch page and workflow overview.
- `/external-scout`: latest active validated External Scout packet review.
- `/external-scout/threads`: 24/7 External Scout Live Case Board over durable topic threads.
- `/rfi`: theater/workspace organization.
- `/rfi/SOCCENT`: thread-current RFI preview with raw-packet fallback.

## Supporting And Audit Surfaces

- `/canonical-cases`: canonical case index and evidence lineage entrypoint.
- `/case-genesis`: dry-run candidate review.
- Evidence passports, OSIR previews, PIR APIs, agent feed, source coverage, and source health are supporting/audit surfaces unless a later task promotes them.

## External Scout Status

- Available: `True`
- Active selection policy: `latest_validated_capture_only`
- Active packet count: `1`
- History packet count: `1133`
- Latest packet timestamp: `2026-07-20T21:03:11Z`
- Stale: `False`
- Read-only: `True`
- Private browser state read: `False`
- Cookies read: `False`
- Local storage read: `False`

## RFI Behavior

RFI uses External Scout Case Thread current state when available, then falls back to the best validated External Scout packet; canonical cases, Case Genesis, source coverage, and provenance remain audit material.

## Global Theater Watch

Global Seven-Theater Watch and rotating deep dives are implemented and have receipt-backed live Packet-output verification. The same-source operator projection reports rows present, theaters swept, verified-complete coverage, candidate-only theaters, performed deep dives, and rotation credits separately. Configured bounded sweep only. This does not assert exhaustive coverage of all world events.

## Capture Bridge

Visible/file-first capture is local-only and feeds staging/quarantine before inbox promotion.

## Local-Only Runtime

The following are local-only and are not mirrored here:

- ChatGPT browser session and visible capture state.
- launchd capture jobs.
- External Scout inbox, latest, staging, quarantine, receipts, and logs.
- Local DB files and DB runtime state.
- Browser cookies, storage, profile files, credentials, tokens, and `.env` values.

## Latest Source Commits

- `76ff624 docs(mirror): remove sanitizer-reserved wording`
- `5fae35f test(ui): execute hostile payload through final DOM redaction`
- `42edc21 fix(agent-room): preserve run source and filter truth`
- `f421c1e test(ui): enforce operator and technical separation`
- `09bcdfd docs(demo): add controlled AUTOSINT briefing package`
- `b20e059 feat(agent-room): improve typed collaboration projection`
- `3247555 feat(pir): improve operator PIR projection`
- `dccf2c1 feat(ui): add operator briefing case and sensor experience`
- `16509cb docs(release): preserve pilot acceptance boundary`
- `9050d29 docs(release): document cleared PostgreSQL and UI gates`
- `f7e43d4 fix(ui): preserve canonical current database state in RFI`
- `cb34103 test(ui): enforce real rendered UAT and screenshot integrity`
- `40571c8 fix(ui): add canonical state and specialized system projections`
- `f37dbae fix(db): build and validate isolated AUTOSINT PostgreSQL`
- `429ac2c fix(db): honor preserved PGDATA for isolated managed PostgreSQL`
- `1cf6680 fix(architecture): refresh canonical registry projections`
- `bd3c60d test(architecture): enforce Production Foundation invariants`
- `9762cbb feat(ui): add feature-flagged operator UI V2 shell`
- `4e9025b docs(ui): define operator-first UI V2`
- `3860652 feat(generation): add replay-enabled ScoutGenerationService`

## Pending Decisions

- Keep the mirror refreshed after major workflow changes.
- Install/load hourly capture only after separate operator approval.
- External Scout Live Case Board v1 is implemented; use /external-scout/threads as the 24/7 thread board.
- Design controlled approval before Evidence or case-link mutation.

## Safety Boundary

- ChatGPT packets are candidate input only, not Evidence.
- Review surfaces do not perform DB writes, raw Evidence mutation, case-link mutation, source-config mutation, OSIR bypass, commander-ready promotion, apply/import actions, launchd install/load/start, or frontend write controls.
- Market, crypto, prediction-market, social, and public-comment material remains cue-only.

## Context URLs

See `docs/status/AUTOSINT_CONTEXT_INDEX.md` for the current raw URL list.
