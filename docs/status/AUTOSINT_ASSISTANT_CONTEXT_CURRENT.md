# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from private AUTOSINT source-of-truth docs and safe local status, without copying runtime artifacts or private browser state.

## Source

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source branch: `main`
- Source HEAD: `c231c97ab1c3c5f2c63437299e3533548ddeabd4`
- Generated at: `2026-06-30T10:35:53Z`

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
- History packet count: `564`
- Latest packet timestamp: `2026-06-30T09:58:30Z`
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

- `c231c97 fix(scout): clarify 24/7 source gap actions`
- `9f42769 fix(scout): preserve late packet recovery and source closures`
- `1e4bec8 fix(ops): keep stale source gaps informational`
- `68d0162 fix(scout): apply latest source gap closures to thread health`
- `eb18958 fix(scout): bound packet readiness copy fallback`
- `60dc8b2 feat(scout): add external scout 24/7 source health proof`
- `65aefa5 docs(scout): record scheduled task replacement blocker`
- `961327f docs(scout): mark scheduled task output path blocked`
- `8f05a70 docs(scout): record scheduled task chat menu risk`
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
