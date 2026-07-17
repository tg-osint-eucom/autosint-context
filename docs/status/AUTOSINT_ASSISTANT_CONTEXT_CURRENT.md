# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from private AUTOSINT source-of-truth docs and safe local status, without copying runtime artifacts or private browser state.

## Source

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source branch: `main`
- Source HEAD: `fe6c0b27e1efbf003abf0a20987ce1e35cead26a`
- Generated at: `2026-07-17T00:30:25Z`

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
- History packet count: `1072`
- Latest packet timestamp: `2026-07-17T00:06:33Z`
- Stale: `False`
- Read-only: `True`
- Private browser state read: `False`
- Cookies read: `False`
- Local storage read: `False`

## RFI Behavior

RFI uses External Scout Case Thread current state when available, then falls back to the best validated External Scout packet; canonical cases, Case Genesis, source coverage, and provenance remain audit material.

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

- `fe6c0b2 fix(ui): describe empty enrichment gate scope`
- `0ea7710 fix(ui): render validation status without runtime artifacts`
- `3f095d0 fix(release): reject override references in final csv`
- `b9ce2dc fix(preservation): distinguish foreign defense stocks`
- `845b4ce fix(release): include final conflict matrix`
- `ab33a80 feat(release): build coherent runtime restore snapshot`
- `7c73e01 test(docs): enforce coherent review snapshots`
- `7339df2 feat(scout): trace semantic fields across operator surfaces`
- `7ba962b fix(contract): enforce structured runtime descriptors`
- `fc0b152 fix(scout): release terminal normalized output guard`
- `06476b8 test(docs): enforce documentation and package consistency`
- `47e1618 docs: consolidate canonical AUTOSINT operating truth`
- `57f8077 fix(sensors): enforce semantic and preservation gates`
- `9f92afe refactor(rfi): consolidate operational preview under RFI`
- `b9333e9 feat(core): add canonical AUTOSINT system contract guard`
- `68c9812 fix(scout): preserve prompt lifecycle and duplicate guards`
- `198bb02 docs(scout): remove private packet identifiers`
- `328abba docs: deprecate legacy and duplicate guidance`
- `ec5be89 docs: align current External Scout and system terminology`
- `2870d6c docs: add canonical AUTOSINT documentation index`

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
