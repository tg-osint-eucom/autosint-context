# AUTOSINT Long-Running Work Model

AUTOSINT work should survive long chats, handoffs, scheduled runs, and context
loss. The durable operating loop is:

```text
finding -> validation -> dedupe -> false-positive check -> targeted fix -> tests -> release surface -> context mirror -> human boundary
```

This model is project-state memory only. It does not create Evidence, link
cases, change source configuration, open OSIR, run apply/import, promote
commander-ready outputs, install launchd jobs, or read private browser state.

## Purpose

AUTOSINT has several active workstreams: External Scout capture, Live Case
Board, strict packet contracts, HAVOC/RFI thread-current behavior, context
mirror freshness, capture isolation, PIR overlays, source policy, and runtime
health. These should be tracked as explicit workstreams with verification gates
instead of being rediscovered from chat history.

The workstream registry is `config/autosint_workstreams.yml`. The human-readable
status surface is `docs/status/AUTOSINT_WORKSTREAMS.md`. Generated report output
belongs under ignored `artifacts/autosint_workstreams/latest/`.

## Workstream Rules

- Each workstream needs a specific `verification_gate` and
  `definition_of_done`.
- `next_action` must be executable by a future Codex run without guessing.
- `risk_boundary` must say what the workstream must not mutate.
- `context_mirror_required` is `true` when a completed change affects the
  public operating context.
- `last_verified_at` and `next_scheduled_check` may be null, but the fields
  must exist.

Valid statuses:

- `Planned`
- `Active`
- `Blocked`
- `Needs Verification`
- `Complete`
- `Archived`

## Verification Examples

- `strict scheduled production cycle proven` means a natural scheduled run promoted a
  strict valid packet with `validation_error_count=0`.
- `Live Case Board current` means route/API checks return 200, `board_summary`
  is present, thread count is nonzero, and latest capture is not stale unless
  the source output itself is stale.
- `context mirror current` means the public mirror includes the latest private
  source-of-truth docs and the mirror sanitization gate passed.
- `HAVOC/RFI thread-current selected` means the HAVOC/RFI preview consumes
  thread current state before raw packet fallback and remains review-only.

## Daybreak / Patch-Style Quality Loop

Use the same rhythm for bugs, stale operations, source drift, or schema drift:

1. Finding: state the observed problem and source.
2. Validation: reproduce from repo/runtime evidence.
3. Dedupe: check whether a workstream already covers it.
4. False-positive check: distinguish stale UI, stale server, bad fixture, or
   expected fail-closed behavior from a real defect.
5. Targeted fix: change the narrowest safe surface.
6. Test: run targeted tests plus compile checks.
7. Release surface: run the release gate when contracts may be affected.
8. Context mirror: refresh the public mirror when operating context changes.
9. Human boundary: stop before DB, Evidence, case-link, source-config, OSIR,
   apply/import, commander-ready, launchd, or private-state changes unless the
   user explicitly approves that exact class of work.

## Safety Boundary

Workstream tracking must never become an apply/import or commander-ready action.
It is a read-only memory and verification layer. It must not:

- mutate DB rows;
- rewrite raw Evidence;
- create case links;
- change source configuration;
- bypass OSIR;
- run apply/import;
- promote commander-ready outputs;
- install/load/start launchd jobs;
- add frontend write controls;
- read cookies, sessions, localStorage, sessionStorage, Chrome profile files,
  credential files, `.env` values, tokens, or private browser state.
