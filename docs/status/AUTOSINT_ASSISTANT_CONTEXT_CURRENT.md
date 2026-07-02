# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from private AUTOSINT source-of-truth docs and safe local status, without copying runtime artifacts or private browser state.

## Source

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source branch: `main`
- Source HEAD: `4a3c26c767d90c2d74fb65e80233735b75d327df`
- Generated at: `2026-07-02T22:16:32Z`

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
- History packet count: `624`
- Latest packet timestamp: `2026-07-02T17:46:10Z`
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

- `4a3c26c fix(scout): fail closed when prompt trigger UI is locked`
- `7eb9212 fix(scout): keep normalized prompt trigger on findings path`
- `b72ab88 feat(scout): normalize pro extended scout findings`
- `7275b51 feat(scout): normalize scout findings into strict packets`
- `6622376 fix(scout): harden stalled response detection`
- `b63a411 fix(ops): reflect telegram session adapter readiness`
- `663c58e fix(ops): synchronize source sensor provider decisions`
- `a480efa fix(ops): add telegram and fmp source adapter checks`
- `eb5cc9f fix(ops): surface source adapter credential status`
- `49a9138 fix(ops): show public prediction adapters in 24-7 proof`
- `50c8142 fix(scout): close hormuz source gaps with read-only adapters`
- `ac659f9 fix(scout): preserve active board during enrichment follow-up`
- `f6b709b fix(scout): keep source-lane enrichment follow-up active`
- `bfa8d32 fix(scout): run signed kalshi enrichment without collapsing board`
- `6af24f8 fix(scout): allow safe accidental packet composer cleanup`
- `8af1952 fix(scout): harden prompt recovery state machine`
- `e15ecf5 feat(ops): add sensor architecture map to 24-7 proof`
- `5ae30c5 fix(ui): show source urls in 24-7 source health`
- `9cb6c4d fix(ops): surface packet stall recovery diagnostics`
- `279f1f5 fix(ui): show retained source health on 24-7 page`

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
