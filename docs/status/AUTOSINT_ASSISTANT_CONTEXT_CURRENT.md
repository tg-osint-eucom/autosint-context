# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from private AUTOSINT source-of-truth docs and safe local status, without copying runtime artifacts or private browser state.

## Source

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source branch: `main`
- Source HEAD: `4f60ddf168ac3d29a99c641b4b27c065896b3524`
- Generated at: `2026-06-28T20:47:54Z`

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
- Active packet count: `5`
- History packet count: `439`
- Latest packet timestamp: `2026-06-28T20:06:30Z`
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

- `4f60ddf docs(scout): record scheduled task output blocker`
- `d3ce97b docs(scout): record scheduled task containment`
- `e7245d4 fix(scout): isolate scheduled task capture probe`
- `dde1a0e docs(scout): record scheduled task upstream proof failure`
- `458a1a5 fix(scout): split scheduled task and fallback targets`
- `54ac575 fix(scout): harden packet target selection for scheduled path`
- `70c480d fix(ops): tune external scout health monitor signals`
- `6211b97 feat(ops): alert on external scout red health`
- `9934bea fix(scout): harden packet extraction and health monitor recovery`
- `bab9fec fix(scout): add external scout health monitor and stale draft cleanup`
- `43af14d chore(export): add case deep-dive handoff exporter`
- `0949cec fix(scout): extend prompt packet readiness window`
- `567d039 fix(scout): harden prompt submit state machine`
- `fe29a90 fix(scout): bind prompt readiness to trigger request id`
- `0e2d0d3 chore(ops): record external scout launchd repair`
- `1506e05 fix(scout): require packet readiness after prompt trigger`
- `e0f10a6 feat(eval): expand AUTOSINT evaluation dataset`
- `e4d56f7 feat(eval): add AUTOSINT evaluation dataset v0`
- `fdf3866 chore(ops): add GPT-5.6 evaluation workstream`
- `13145a2 fix(scout): run finance enrichment after new captures`

## Source Dirty State

- clean

## Pending Decisions

- Keep the mirror refreshed after major workflow changes.
- Install/load hourly capture only after separate operator approval.
- External Scout Live Case Board v1 is implemented; use /external-scout/threads as the 24/7 thread board.
- Global sensor coverage policy is implemented; theater_watch_summary still needs live Packet-output verification.
- Design controlled approval before Evidence or case-link mutation.

## Safety Boundary

- ChatGPT packets are candidate input only, not Evidence.
- Review surfaces do not perform DB writes, raw Evidence mutation, case-link mutation, source-config mutation, OSIR bypass, commander-ready promotion, apply/import actions, launchd install/load/start, or frontend write controls.
- Market, crypto, prediction-market, social, and public-comment material remains cue-only.

## Context URLs

See `docs/status/AUTOSINT_CONTEXT_INDEX.md` for the current raw URL list.
