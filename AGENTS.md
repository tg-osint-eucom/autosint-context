# AUTOSINT Codex Instructions

These instructions are the durable repo-level operating rules for Codex work in AUTOSINT.

## AUTOSINT Standing Autopush Policy

Codex may stage, commit, and push automatically after implementation when the autopush gate passes.

Codex must stop and ask the user when:

- the task explicitly says no commit, no push, or Plan Mode;
- validation fails;
- the diff boundary is mixed or unclear;
- unrelated files appear;
- forbidden files appear;
- secrets or private data might be involved;
- DB/schema/source-config/OSIR/apply/import behavior changes without explicit approval;
- remote/branch/push target is unclear.

### Autopush Gate

Before staging, Codex must confirm:

1. Boundary is clean.

   - Staged files must match the task scope exactly.
   - Do not use `git add .`.
   - Use hunk staging when needed.
   - Stop if unrelated files or mixed hunks cannot be separated safely.

2. Validation is green.

   Required by default:

   - `git diff --check`
   - targeted pytest for changed area
   - `py_compile` for changed Python files
   - release surface validation when available or requested

3. Forbidden files are not staged.

   Never stage or push:

   - `.env` or `.env.*`
   - secrets
   - tokens
   - credential files
   - browser profile files
   - cookies
   - localStorage/sessionStorage
   - DB files
   - `artifacts/*`
   - screenshots
   - logs
   - patch backups
   - External Scout inbox/latest/staging/quarantine/receipts/logs
   - `docs/AUTOSINT_SOURCE_CATALOG.md` unless explicitly approved

4. Risky mutation classes require explicit approval.

   Stop before commit/push if the task changes:

   - DB schema/migrations
   - source registry/config
   - apply/import path
   - OSIR gate behavior
   - commander-ready promotion
   - Evidence writes
   - case-link writes
   - credential handling
   - browser private-state access

5. Final report must include:

   - branch
   - commit hash
   - push result
   - files committed
   - validation summary
   - route smoke summary if applicable
   - current dirty state
   - confirmation no DB mutation
   - confirmation no raw Evidence mutation
   - confirmation no case-link mutation
   - confirmation no source-config mutation
   - confirmation no OSIR bypass
   - confirmation no apply/import path
   - confirmation generated artifacts remained ignored/uncommitted
   - confirmation `docs/AUTOSINT_SOURCE_CATALOG.md` remained untouched/untracked unless explicitly approved
   - confirmation no secrets/private browser state were read or printed

### Push Behavior

If the current repo is the clean AUTOSINT repo and the gate passes:

- commit with a conventional commit message;
- push the current branch to origin.

For larger or risky features:

- use a feature branch if appropriate;
- push branch;
- report PR/opening instructions if available.

Conventional commit examples:

- `feat(...)`
- `fix(...)`
- `chore(...)`
- `docs(...)`
- `test(...)`
