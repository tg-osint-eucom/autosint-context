# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from private AUTOSINT source-of-truth docs and safe local status, without copying runtime artifacts or private browser state.

## Source

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source branch: `main`
- Source HEAD: `557c0f4a40bef06f424a3834bb0ca5e12aa9a488`
- Generated at: `2026-07-06T22:49:59Z`

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
- History packet count: `800`
- Latest packet timestamp: `2026-07-06T22:04:52Z`
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

- `557c0f4 fix(ui): keep autosint app navigation local`
- `3c3e87a fix(ui): rename external scout cockpit title`
- `b8e874c fix(scout): expand next-run source gap targets`
- `8904ab2 fix(scout): run source-gap closure after harvest`
- `f5f7c52 docs(ops): remove legacy external scout capture language`
- `7ee67ac fix(ops): remove external scout direct capture fallback`
- `d50ac9f feat(ops): add source lane green gate export`
- `9d0c977 docs(scout): record packet v2 stale draft recovery`
- `1e7f6f0 fix(ops): treat pending scout findings as nonblocking`
- `346db20 fix(scout): clear stale autosint draft safely`
- `6b670f5 fix(scout): feed source-gap targets into findings prompt`
- `88077c2 fix(ops): recover packet v2 renderer harvest`
- `197d551 fix(ops): split scout submit from async harvest`
- `4b48a73 test(scout): assert keep-open renderer default`
- `b945e8f fix(scout): keep packet v2 open for async harvest`
- `43e881d fix(scout): wait for packet v2 harvest readiness`
- `aa9f6b3 style(ui): apply black mesa external scout skin`
- `4aa60d6 fix(ui): compact external scout cockpit`
- `e799882 fix(scout): close packet tab on harvester timeout`
- `75280d5 fix(scout): add packet v2 renderer hygiene`

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
