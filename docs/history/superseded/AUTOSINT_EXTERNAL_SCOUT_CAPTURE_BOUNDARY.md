# AUTOSINT External Scout Capture Boundary

- Status: Archived superseded historical implementation boundary; direct capture is manual-only
- Authority: Supporting boundary, not production schedule authority
- Version: 1.0
- Owner: External Scout capture package
- Last reviewed: 2026-07-15
- Archived at: 2026-07-19
- Original path: `docs/AUTOSINT_EXTERNAL_SCOUT_CAPTURE_BOUNDARY.md`
- Runtime truth: No
- Supersedes: None
- Superseded by: [External Scout Runbook](../../AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md) for current production timing and output mode
- Related: [Primary Workflow](../../AUTOSINT_PRIMARY_WORKFLOW.md), [Documentation Conflicts](../../status/AUTOSINT_DOCUMENTATION_CONFLICTS.md)

This document preserves the direct-capture package boundary. It does not define
the current production loop. The production loop is prompt at `:00`, async
harvester at `:28`, Scout Findings normalization, validation, and promotion.
Direct capture remains manual diagnostic or emergency tooling only.

## Responsibility

The External Scout capture subsystem is the local bridge between the visible ChatGPT `AUTOSINT External Scout` Project output and AUTOSINT's read-only packet review artifacts.

It is implemented as a service-ready package inside this repo:

```text
src/autosint_external_scout_capture/
```

The historical/manual wrapper remains:

```text
scripts/run_external_scout_capture_once.sh
```

The legacy script path remains as a compatibility shim:

```text
scripts/capture_chatgpt_external_scout_visible.py
```

## Inputs

Allowed inputs:

- Visible ChatGPT Project tab text.
- Visible ChatGPT JSON/Markdown file attachments when available.
- Existing ignored External Scout runtime artifacts needed for recency, duplicate detection, and status.

Forbidden inputs:

- Cookies.
- Sessions.
- `localStorage` or `sessionStorage`.
- Tokens.
- Chrome profile files.
- Credential files.
- `.env` values.
- Private browser state.

## Outputs

Allowed outputs are ignored local runtime artifacts only:

- `artifacts/external_scout/staging/`
- `artifacts/external_scout/inbox/`
- `artifacts/external_scout/quarantine/`
- `artifacts/external_scout/capture_receipts/`
- `artifacts/external_scout/capture_logs/`
- `artifacts/external_scout/latest/`

Capture writes through staging first. Valid packets promote to inbox only when validation errors are zero. Invalid or malformed captures go to quarantine or raw fallback. Duplicate or older visible output writes a receipt and skips promotion.

## Forbidden Actions

The capture subsystem must not:

- Mutate DB rows.
- Create or modify raw Evidence.
- Create case links.
- Change source config or source registries.
- Bypass OSIR.
- Perform apply/import.
- Open commander-ready gates.
- Add frontend write controls.
- Call API/UI/RFI internals directly.

## Consumption Boundary

AUTOSINT core surfaces consume validated packet reports and thread reports only.

- `core/api.py` renders packet/thread review surfaces.
- Case Threads group validated packet history.
- RFI consumes thread current state first and packet fallback second.

Those layers should not call AppleScript, Chrome automation, launchd logic, or browser-visible capture code.

## CLI Contract

Preferred CLI:

```bash
PYTHONPATH=src:. .venv/bin/python -m autosint_external_scout_capture.cli --status
PYTHONPATH=src:. .venv/bin/python -m autosint_external_scout_capture.cli --once --prefer-files
PYTHONPATH=src:. .venv/bin/python -m autosint_external_scout_capture.cli --once --dry-run
```

Compatibility CLI:

```bash
.venv/bin/python scripts/capture_chatgpt_external_scout_visible.py --status
```

## Historical Launchd Behavior (Superseded)

The package was originally designed around this launchd label:

```text
com.autosint.external-scout-capture
```

The retired design schedule was:

```text
minute :00 each hour (superseded; not the production schedule)
```

Do not use this label as a scheduled production fallback. Current production
timing is owned by the prompt trigger and async harvester described in the
runbook. A manually approved diagnostic invocation may call the package CLI and
write ignored capture logs in the Aqua user session; it must not inspect browser
storage.

The legacy `com.autosint.operator.scheduler` should remain disabled.

## Receipts And Failure Modes

Every successful, skipped, quarantined, or capture-unavailable run should produce a receipt unless the wrapper itself cannot start.

Important receipt states:

- `promoted_to_inbox=true`: valid newer packet set promoted.
- `capture_skipped=true`: duplicate, older, or capture-unavailable event skipped safely.
- `validation_failed=true`: staged JSON failed packet validation and was quarantined unless explicitly overridden.
- `capture_error`: bounded capture failure such as AppleScript timeout.

All receipt privacy and mutation flags must remain false.

## Manual Diagnostic Commands

Commands that use `--once` or the wrapper can interact with visible browser UI
and require explicit current-task approval. They do not count toward natural
production proof. Read-only status/report commands remain the preferred audit
path.

```bash
PYTHONPATH=src:. .venv/bin/python -m autosint_external_scout_capture.cli --status
PYTHONPATH=src:. .venv/bin/python -m autosint_external_scout_capture.cli --once --dry-run --prefer-files
scripts/run_external_scout_capture_once.sh --prefer-files
launchctl print gui/$(id -u)/com.autosint.external-scout-capture
.venv/bin/python scripts/report_external_scout_threads.py --dry-run
```

Route smoke:

```text
/mission-control
/external-scout
/external-scout/threads
/api/v1/external-scout/threads
/rfi/SOCCENT
/api/v1/rfi/SOCCENT
```

## Future Separate Service Criteria

Only consider extracting this subsystem to a separate repo or service when all are true:

- The CLI contract is stable.
- Capture tests pass independently.
- The package has no imports from `core/api.py` or RFI internals.
- Launchd calls only the package CLI.
- Capture output schema is versioned.
- Context mirror and runbooks document the boundary.
- There is a concrete operational need for independent release or deploy.
