# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from private AUTOSINT source-of-truth docs and safe local status, without copying runtime artifacts or private browser state.

## Source

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source branch: `main`
- Source HEAD: `00e9ebc18b1330e39d616f7c106e98b18d88782c`
- Generated at: `2026-06-23T18:34:46Z`

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
- History packet count: `43`
- Latest packet timestamp: `2026-06-23T18:03:01Z`
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

- `00e9ebc fix(scout): require current multilingual context for preview readiness`
- `b330a72 fix(scout): separate current thread status from historical warnings`
- `7169a7f fix(ui): make live case board the primary first read`
- `c35e9de fix(ui): keep live board audit details out of operator path`
- `bed03f1 fix(scout): improve live case board correctness`
- `892dc9e chore(ops): verify strict external scout capture workstream`
- `e7628fb fix(scout): extend launchd capture timeouts`
- `720e628 fix(scout): target external scout daily task capture`
- `0a1bcad feat(ops): add AUTOSINT long-running work loop`
- `27a32e9 chore(context): mirror ChatGPT project operating model`
- `93d1d28 docs: define AUTOSINT ChatGPT project operating model`
- `570e415 fix(scout): accept structured source family statuses`
- `2948f10 feat(scout): require full case coverage matrix`
- `30f0477 fix(scout): tolerate safe external scout schema drift`
- `23f61cf fix(ui): keep mission control launch page responsive`
- `0e349f1 docs: mark external scout live board current`
- `eb265cb feat(scout): add external scout live case board`
- `83d63c2 Merge pull request #1 from tg-osint-eucom/feat/external-scout-capture-isolation`
- `c439c64 refactor(scout): isolate external scout capture subsystem`
- `7e21893 fix(scout): harden scheduled external scout capture`

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
