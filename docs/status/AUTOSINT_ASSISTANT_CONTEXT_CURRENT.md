# AUTOSINT Assistant Context Current

This is a public, sanitized context file for restoring AUTOSINT project context in ChatGPT/Codex. It is derived from the current private AUTOSINT operating docs and sanitized local assistant context.

## Source Repo

- Private code/runtime repo: `tg-osint-eucom/autosint`
- Public context mirror: `tg-osint-eucom/autosint-context`
- Source commit used for this mirror: `bcc4baa2f838e66930a65503342313bdf7ec37b2`

## Primary Workflow

`Mission Control -> External Scout -> TSOC/HAVOC -> HAVOC/RFI -> future controlled approval`

## Primary Route Roles

- `/mission-control`: operator launch page and workflow overview.
- `/external-scout`: latest active validated External Scout packet review.
- `/tsoc-havoc`: theater/workspace organization.
- `/havoc-rfi/SOCCENT`: packet-driven HAVOC/RFI preview.

## Supporting And Audit Surfaces

- `/canonical-cases`: canonical case index and evidence lineage entrypoint.
- `/case-genesis`: dry-run candidate review.
- Evidence passports, OSIR previews, PIR APIs, agent feed, source coverage, and source health are supporting/audit surfaces unless a later task promotes them.

## External Scout Current Model

- ChatGPT scheduled scouting produces candidate packets.
- AUTOSINT captures visible/file-first output locally.
- Captures land in staging first.
- Valid captures are promoted to inbox.
- Invalid captures are quarantined.
- Default active review uses the latest validated capture only.
- Older captures remain history and require explicit history mode.

## HAVOC/RFI Behavior

HAVOC/RFI is packet-driven when a suitable validated External Scout packet exists. Canonical cases, Case Genesis, TSOC/HAVOC, source coverage, and provenance remain audit/provenance material.

## Safety Boundary

- ChatGPT packets are candidate input only, not Evidence.
- Review surfaces do not perform DB writes, raw Evidence mutation, case-link mutation, source-config mutation, OSIR bypass, commander-ready promotion, apply/import actions, launchd install/load/start, or frontend write controls.
- Market, crypto, prediction-market, social, and public-comment material remains cue-only.

## Local-Only Runtime

The following are local-only and are not mirrored here:

- ChatGPT browser session and visible capture state.
- launchd capture jobs.
- External Scout inbox, latest, staging, quarantine, receipts, and logs.
- Local DB files and DB runtime state.
- Browser cookies, storage, profile files, credentials, tokens, and `.env` values.

## Pending Decisions

- Keep this public mirror synchronized with sanitized operating context after major workflow changes.
- Use the private `autosint` repo for code and tests.
- Use this mirror only for context alignment when private connector access is unreliable.
- Do not add code, generated artifacts, raw Evidence, DB content, source catalog content, screenshots, logs, or secrets to this mirror without explicit approval.

## Files To Read When Context Is Lost

- `README.md`
- `AGENTS.md`
- `docs/AUTOSINT_OPERATING_MODEL_CURRENT.md`
- `docs/AUTOSINT_PRIMARY_WORKFLOW.md`
- `docs/AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md`
- `docs/status/AUTOSINT_ASSISTANT_CONTEXT_CURRENT.md`
