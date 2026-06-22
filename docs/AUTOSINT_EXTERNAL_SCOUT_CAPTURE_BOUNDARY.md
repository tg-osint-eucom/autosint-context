# AUTOSINT External Scout Capture Boundary

## Responsibility

The External Scout capture subsystem is the local bridge between the visible ChatGPT `AUTOSINT External Scout` Project output and AUTOSINT's read-only packet review artifacts.

It is implemented as a service-ready package inside this repo:

```text
src/autosint_external_scout_capture/
```

The launchd wrapper remains:

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
- Call API/UI/HAVOC/RFI internals directly.

## Consumption Boundary

AUTOSINT core surfaces consume validated packet reports and thread reports only.

- `core/api.py` renders packet/thread review surfaces.
- Case Threads group validated packet history.
- HAVOC/RFI consumes thread current state first and packet fallback second.

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

## Launchd Behavior

Launchd label:

```text
com.autosint.external-scout-capture
```

Schedule:

```text
minute :08 each hour
```

The wrapper calls the package CLI and writes wrapper logs under ignored capture logs. The job should run in the Aqua user session so AppleScript can reach visible Chrome UI. It must not inspect browser storage.

The legacy `com.autosint.operator.scheduler` should remain disabled.

## Receipts And Failure Modes

Every successful, skipped, quarantined, or capture-unavailable run should produce a receipt unless the wrapper itself cannot start.

Important receipt states:

- `promoted_to_inbox=true`: valid newer packet set promoted.
- `capture_skipped=true`: duplicate, older, or capture-unavailable event skipped safely.
- `validation_failed=true`: staged JSON failed packet validation and was quarantined unless explicitly overridden.
- `capture_error`: bounded capture failure such as AppleScript timeout.

All receipt privacy and mutation flags must remain false.

## Manual Proof Commands

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
/havoc-rfi/SOCCENT
/api/v1/havoc-rfi/SOCCENT
```

## Future Separate Service Criteria

Only consider extracting this subsystem to a separate repo or service when all are true:

- The CLI contract is stable.
- Capture tests pass independently.
- The package has no imports from `core/api.py` or HAVOC/RFI internals.
- Launchd calls only the package CLI.
- Capture output schema is versioned.
- Context mirror and runbooks document the boundary.
- There is a concrete operational need for independent release or deploy.
