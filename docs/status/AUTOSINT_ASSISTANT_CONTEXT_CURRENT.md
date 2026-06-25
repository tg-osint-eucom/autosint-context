# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from private AUTOSINT source-of-truth docs and safe local status, without copying runtime artifacts or private browser state.

## Source

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source branch: `main`
- Source HEAD: `3f7d1996f7c16cdb8a9f82481467ad64b15809b3`
- Generated at: `2026-06-25T02:33:28Z`

## Primary Workflow

`Mission Control -> External Scout -> TSOC/HAVOC -> HAVOC/RFI -> future controlled approval`

## Primary Route Roles

- `/mission-control`: operator launch page and workflow overview.
- `/external-scout`: latest active validated External Scout packet review.
- `/external-scout/threads`: 24/7 External Scout Live Case Board over durable topic threads.
- `/tsoc-havoc`: theater/workspace organization.
- `/havoc-rfi/SOCCENT`: thread-current HAVOC/RFI preview with raw-packet fallback.

## Supporting And Audit Surfaces

- `/canonical-cases`: canonical case index and evidence lineage entrypoint.
- `/case-genesis`: dry-run candidate review.
- Evidence passports, OSIR previews, PIR APIs, agent feed, source coverage, and source health are supporting/audit surfaces unless a later task promotes them.

## External Scout Status

- Available: `True`
- Active selection policy: `latest_validated_capture_only`
- Active packet count: `4`
- History packet count: `69`
- Latest packet timestamp: `2026-06-25T01:28:50Z`
- Stale: `False`
- Read-only: `True`
- Private browser state read: `False`
- Cookies read: `False`
- Local storage read: `False`

## HAVOC/RFI Behavior

HAVOC/RFI uses External Scout Case Thread current state when available, then falls back to the best validated External Scout packet; canonical cases, Case Genesis, TSOC/HAVOC, source coverage, and provenance remain audit material.

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

- `3f7d199 feat(scout): support multi-case live board`
- `c6de334 chore(ops): record prompt trigger short-loop proof`
- `5e78beb fix(scout): avoid prompt trigger response false positives`
- `8779669 chore(ops): record external scout natural cycle proof`
- `81e88fe docs: add AUTOSINT orchestration roadmap`
- `ce6c6eb fix(scout): harden prompt trigger verification`
- `dc933d0 fix(scout): target visible ChatGPT composer for prompt trigger`
- `854c69f fix(scout): improve scheduled prompt trigger reliability`
- `c10f661 fix(scout): stabilize prompt trigger composer submit`
- `9ed368e fix(scout): remove keystroke dependency from prompt trigger`
- `a5e9bad fix(scout): require verified prompt trigger delivery`
- `6b6116f fix(scout): harden prompt trigger submission`
- `924fa0c fix(scout): verify prompt trigger submission`
- `a7b6632 fix(scout): harden launchd prompt trigger submit`
- `8b06ac0 feat(scout): add local external scout prompt trigger`
- `8fbcaff fix(scout): require exact packet chat target for launchd capture`
- `340fa0e fix(ui): separate HAVOC current coverage from legacy linkage audit`
- `f3b6e4e fix(scout): preserve best thread current state across lower quality updates`
- `76efc6e chore(debug): add read-only page dump utility`
- `f9147d6 fix(ui): clean remaining operator path audit leakage`

## Source Dirty State

- clean

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
