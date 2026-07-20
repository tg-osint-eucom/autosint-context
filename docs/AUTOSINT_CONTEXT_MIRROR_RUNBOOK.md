# AUTOSINT Context Mirror Runbook

- Status: Current runbook
- Authority: Canonical sanitized context-mirror publication procedure
- Version: 2.1
- Owner: AUTOSINT Documentation
- Last reviewed: 2026-07-19
- Supersedes: Ad hoc hard-coded mirror document selection
- Superseded by: None
- Runtime truth: No; the public mirror is recovery context and does not prove current local runtime

The public context mirror keeps sanitized AUTOSINT operating context available to ChatGPT/Codex when private GitHub connector access is unavailable.

Mirror repo:

```text
https://github.com/tg-osint-eucom/autosint-context
```

Private source repo:

```text
https://github.com/tg-osint-eucom/autosint
```

## Purpose

The mirror is documentation-only. It contains current operating context, workflow references, runbook content, and a raw URL index. It does not contain code, generated artifacts, DB files, raw Evidence, External Scout inbox data, browser state, logs, screenshots, credentials, tokens, or `.env` values.

## Codex Context And Memory Rule

Codex memories are helper recall only. They are useful for orientation, but
durable AUTOSINT operating rules must live in `AGENTS.md` or tracked docs and
then be published to this sanitized context mirror when relevant.

Use the current ChatGPT/Codex thread only as temporary working context. Use
`/goal` for substantial AUTOSINT work so the objective, validation gates, and
stop conditions are explicit.

When Codex memory support is available, enable it with:

```toml
[features]
memories = true
```

After meaningful private repo commits that change workflow, architecture,
validation status, or operator behavior, run this mirror workflow so ChatGPT can
restore from public raw URLs instead of relying on chat memory.

## Files Published

The allowlist is derived deterministically from three bounded groups:

1. `README.md` and `AGENTS.md`;
2. every `documents` row with `mirror_input: true` in
   `config/autosint_documentation_authority.yml`;
3. the generated assistant context/index files and the exact config set
   `config/autosint_system_contract.yml`,
   `config/autosint_sensor_architecture.yml`, and
   `config/autosint_documentation_authority.yml`.

`scripts/check_autosint_documentation_authority.py` compares the selected
documentation set with the publisher constant and fails on drift. The archived
`docs/history/superseded/AUTOSINT_EXTERNAL_SCOUT_CAPTURE_BOUNDARY.md` remains an
explicit historical mirror input; publication relocates the old public path as
one tracked move pair. Target and proposal documents are mirrored only when the
registry explicitly opts them in, and their metadata must say that they are not
runtime truth.

`docs/AUTOSINT_SOURCE_CATALOG.md` is a reserved, non-public reference. Its
intentional absence from this mirror and from sanitized review packages is not
an ordinary broken link. Do not create a placeholder or mirror it unless a
separate task explicitly approves that exact source-catalog boundary.

## Commands

Dry-run first:

```bash
.venv/bin/python scripts/publish_autosint_context_mirror.py --dry-run
```

Check status:

```bash
.venv/bin/python scripts/publish_autosint_context_mirror.py --status
```

Publish after the dry-run sanitization gate passes:

```bash
.venv/bin/python scripts/publish_autosint_context_mirror.py --publish
```

The default mode is dry-run. Publish stages only the allowed mirror file set, commits with:

```text
docs: refresh AUTOSINT context mirror
```

and pushes to `origin/main` in the mirror repo.

## Sanitization Gate

The script publishes committed source state only. It fails before write,
commit, or push when any allowlisted source file is dirty or untracked, or when
candidate mirror files include:

- `.env` paths or values.
- token-like, credential-like, or private-key values.
- cookie/session/localStorage/sessionStorage values.
- DB dumps or SQL table/insert dumps.
- generated artifact path content.
- External Scout inbox/latest/staging/quarantine/receipt/log content.
- raw Evidence payload dumps.
- source catalog content unless explicitly approved.
- absolute private local paths.

Boundary text that says these things must not be included is allowed. Secret values and runtime dumps are not.

## Raw URL Index

The generated index is:

```text
https://raw.githubusercontent.com/tg-osint-eucom/autosint-context/main/docs/status/AUTOSINT_CONTEXT_INDEX.md
```

Use that file when ChatGPT needs a compact list of public context URLs.

## Operating Boundaries

This workflow does not mutate DB rows, raw Evidence, case links, source config, OSIR state, apply/import paths, launchd state, browser state, or runtime artifacts. It only publishes sanitized docs to the public context mirror.
