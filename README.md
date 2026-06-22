# AUTOSINT Context Mirror

This repository is a public, sanitized context mirror for ChatGPT/Codex alignment.

The private runtime/code repository is `tg-osint-eucom/autosint`. Use this mirror when a ChatGPT or GitHub connector cannot read the private repo, or when project context needs to be restored quickly without exposing local runtime state.

## What This Mirror Contains

- Repo-level Codex operating instructions in `AGENTS.md`.
- Current AUTOSINT operating model.
- Primary workflow reference.
- External Scout runbook.
- ChatGPT Project operating model.
- Long-running workstream model.
- External Scout capture boundary.
- Workstream status summary.
- Sanitized assistant context status.
- Raw URL index for fast ChatGPT ingestion.

## What This Mirror Does Not Contain

This repository intentionally excludes:

- Application code.
- Generated artifacts.
- External Scout inbox, latest, staging, quarantine, capture receipt, or log files.
- DB files, DB dumps, raw Evidence rows, or case-link runtime data.
- `.env` files, credentials, tokens, cookies, browser profile files, or browser storage.
- Screenshots and local logs.
- `docs/AUTOSINT_SOURCE_CATALOG.md`, unless separately approved later.

## Current AUTOSINT Workflow

`Mission Control -> External Scout -> TSOC/HAVOC -> HAVOC/RFI -> future controlled approval`

AUTOSINT treats ChatGPT External Scout packets as candidate input only. Packets are validated, normalized, deduplicated, and reviewed before any future controlled approval path. Market, crypto, prediction-market, social, and public-comment material remains cue-only context.

## How To Use This Repo

For context recovery, read these files in order:

1. `AGENTS.md`
2. `docs/AUTOSINT_OPERATING_MODEL_CURRENT.md`
3. `docs/AUTOSINT_PRIMARY_WORKFLOW.md`
4. `docs/AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md`
5. `docs/AUTOSINT_CHATGPT_PROJECT_OPERATING_MODEL.md`
6. `docs/AUTOSINT_LONG_RUNNING_WORK_MODEL.md`
7. `docs/AUTOSINT_EXTERNAL_SCOUT_CAPTURE_BOUNDARY.md`
8. `docs/status/AUTOSINT_WORKSTREAMS.md`
9. `docs/status/AUTOSINT_ASSISTANT_CONTEXT_CURRENT.md`
10. `docs/status/AUTOSINT_CONTEXT_INDEX.md`

This repo is documentation-only. Do not treat it as a runtime source, package source, artifact store, or evidence store.
