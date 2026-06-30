# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from private AUTOSINT source-of-truth docs and safe local status, without copying runtime artifacts or private browser state.

## Source

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source branch: `main`
- Source HEAD: `dcebdb3c12ff489be10f2da7c16e1fde800d4af6`
- Generated at: `2026-06-30T13:10:23Z`

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
- History packet count: `568`
- Latest packet timestamp: `2026-06-30T10:58:30Z`
- Stale: `True`
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

- `dcebdb3 fix(scout): fail closed hung prompt trigger recovery`
- `281429a fix(ui): surface 24/7 proof counters and source health`
- `8b6085b fix(scout): clarify per-case source health blockers`
- `ff42103 fix(scout): summarize active source health todos`
- `510cb56 fix(scout): surface warn source causes on 24-7 page`
- `4006336 fix(scout): allow late packet readiness recovery`
- `97faffc fix(scout): expose source recovery verification stages`
- `12346d8 fix(scout): show per-case source verification stages`
- `21daeeb fix(scout): show read-only source verification stage`
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
