# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from private AUTOSINT source-of-truth docs and safe local status, without copying runtime artifacts or private browser state.

## Source

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source branch: `main`
- Source HEAD: `ac659f97d6186377ce9951df5180501dcffd6436`
- Generated at: `2026-07-01T15:50:12Z`

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
- Active packet count: `1`
- History packet count: `601`
- Latest packet timestamp: `2026-07-01T14:39:51Z`
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

- `ac659f9 fix(scout): preserve active board during enrichment follow-up`
- `f6b709b fix(scout): keep source-lane enrichment follow-up active`
- `bfa8d32 fix(scout): run signed kalshi enrichment without collapsing board`
- `6af24f8 fix(scout): allow safe accidental packet composer cleanup`
- `8af1952 fix(scout): harden prompt recovery state machine`
- `e15ecf5 feat(ops): add sensor architecture map to 24-7 proof`
- `5ae30c5 fix(ui): show source urls in 24-7 source health`
- `9cb6c4d fix(ops): surface packet stall recovery diagnostics`
- `279f1f5 fix(ui): show retained source health on 24-7 page`
- `b7f7ff7 fix(scout): expose per-case 24-7 source health counts`
- `a50ce4a fix(scout): recover stalled packet prompt responses`
- `a65ed0c fix(scout): use minimal recovery when prompt generation stalls`
- `dcebdb3 fix(scout): fail closed hung prompt trigger recovery`
- `281429a fix(ui): surface 24/7 proof counters and source health`
- `8b6085b fix(scout): clarify per-case source health blockers`
- `ff42103 fix(scout): summarize active source health todos`
- `510cb56 fix(scout): surface warn source causes on 24-7 page`
- `4006336 fix(scout): allow late packet readiness recovery`
- `97faffc fix(scout): expose source recovery verification stages`
- `12346d8 fix(scout): show per-case source verification stages`

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
