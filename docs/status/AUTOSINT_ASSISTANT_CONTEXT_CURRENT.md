# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from private AUTOSINT source-of-truth docs and safe local status, without copying runtime artifacts or private browser state.

## Source

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source branch: `main`
- Source HEAD: `13145a2e2d4eff7c571c5f7a72deb980e81e1ead`
- Generated at: `2026-06-26T17:45:45Z`

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
- History packet count: `253`
- Latest packet timestamp: `2026-06-26T17:33:07Z`
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

- `13145a2 fix(scout): run finance enrichment after new captures`
- `d871196 feat(scout): add Kalshi read-only enrichment`
- `95167ff fix(scout): canonicalize stale retained threads`
- `e367902 fix(scout): preserve finance enrichment across capture cycles`
- `cce3205 docs: sanitize Codex host instructions for context mirror`
- `3a2a443 docs: update Codex host instructions for current AUTOSINT`
- `d2f4e13 docs: persist Codex memory source-of-truth rule`
- `6b9f1ba fix(scout): preserve stronger market cues during enrichment`
- `5a10656 feat(scout): add market prediction finance enrichment`
- `e0503ae fix(scout): clarify theater watch overflow reasons`
- `0d10cd6 chore(ops): record theater watch natural proof`
- `eee7031 fix(scout): normalize theater watch summary output`
- `5e79e3d fix(scout): harden external scout prompt trigger verification`
- `5d8fddb feat(scout): add global sensor coverage to live board`
- `1d41aa1 fix(scout): clarify coverage versus source checks`
- `d7bd727 chore(ops): verify natural multi-case live board cycle`
- `aebbb4d chore(ops): record multi-case short-loop proof`
- `3f7d199 feat(scout): support multi-case live board`
- `c6de334 chore(ops): record prompt trigger short-loop proof`
- `5e78beb fix(scout): avoid prompt trigger response false positives`

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
