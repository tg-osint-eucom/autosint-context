# AUTOSINT ChatGPT-Codex Handoff Queue

- Status: Current supporting workflow
- Authority: Canonical sanitized file-handoff boundary
- Version: 2.1
- Owner: AUTOSINT Operations
- Last reviewed: 2026-07-19
- Supersedes: Manual private-chat scraping and unbounded handoff exports
- Superseded by: None
- Runtime truth: No; queued files are review inputs and never prove live runtime

## Purpose

This document defines a safe file-based handoff queue for moving sanitized
ChatGPT architecture or operator review into Codex task form without scraping
private ChatGPT chats, browser state, cookies, sessions, localStorage,
sessionStorage, Chrome profile files, tokens, credentials, `.env` values, or
Codex private thread state.

The handoff queue replaces the fragile manual loop:

```text
Codex output -> manual ChatGPT System Control review -> manual copy back to Codex
```

with:

```text
sanitized review file -> local validator -> codex_ready_prompt.md -> manual Codex paste
```

V0 is copy-safe only. It does not post to ChatGPT or Codex automatically.

## Queue Layout

Input:

```text
artifacts/chatgpt_codex_handoff/inbox/
```

Output:

```text
artifacts/chatgpt_codex_handoff/latest/codex_ready_prompt.md
artifacts/chatgpt_codex_handoff/latest/handoff_manifest.json
```

Generated queue files are ignored artifacts. They are not committed.

## Allowed Input

The user may place sanitized Markdown or JSON review files in the inbox.
Allowed input should include:

- title;
- source chat label, such as `AUTOSINT System Control`;
- review summary;
- recommended Codex task;
- safety boundary;
- referenced repo files or artifact names, after sanitization.

Do not include private ChatGPT URLs, browser exports, cookies, sessions,
localStorage/sessionStorage, Chrome profile paths, tokens, credentials, `.env`
values, DB rows, raw Evidence bodies, source catalog content, screenshots, or
runtime capture payloads.

## Script Behavior

`scripts/prepare_codex_handoff_from_chatgpt_review.py`:

- reads Markdown/JSON files from the inbox;
- validates forbidden content patterns;
- extracts a title, source chat label, summary, recommended Codex task, safety
  boundary, and referenced files;
- writes `codex_ready_prompt.md` and `handoff_manifest.json`;
- never opens a browser;
- never uses AppleScript or System Events;
- never uses the clipboard;
- never posts to Codex or ChatGPT.

## Future Automation Boundary

Automatic posting to a Codex thread is not approved in v0. It may be considered
only after an official non-private-state Codex CLI/API/SDK path is verified and
the user explicitly approves the exact path.

The handoff queue does not mutate DB, Evidence, case links, source config,
OSIR, apply/import paths, commander-ready state, launchd jobs, production
prompts, or capture behavior.
