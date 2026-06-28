# AUTOSINT ChatGPT Project Operating Model

This document defines how the ChatGPT Project named `AUTOSINT External Scout`
is used with AUTOSINT. The core rule is simple:

```text
AUTOSINT threads are the case memory. ChatGPT chats are workspaces.
```

The source of truth for current cases is AUTOSINT, especially the External
Scout Live Case Board. ChatGPT Project chats help generate, discuss, or inspect
candidate material, but they are not the durable case database, not Evidence,
not OSIR, and not commander-ready authority.

## Purpose

The ChatGPT Project is the scout and workbench environment for AUTOSINT. It is
used to produce strict External Scout candidate packets, manage system/admin
discussion, and optionally support human-created case deep dives.

It must not become one giant mixed chat, and it must not become one automatic
chat per case or per hourly packet.

## Chat Roles

Exactly three chat types are allowed in the project model.

### AUTOSINT Daily External Scout

`AUTOSINT Daily External Scout` is the scheduled task and machine-output chat.

Purpose:

- Generate hourly strict External Scout packets. The target production model is
  ChatGPT Scheduled Tasks as the primary upstream generator once proven.
- Output strict JSON/Markdown only.
- Feed the visible capture bridge, staging gate, validator, quarantine path,
  active inbox, and Live Case Board.

Rules:

- Do not use this chat for manual discussion.
- Do not ask follow-up questions.
- Do not explain the schema outside the packet output.
- Do not rely on Project files being available to the scheduled task.
- Output file-first JSON/Markdown when available; otherwise fenced JSON first
  and fenced Markdown second.
- Include the full strict coverage contract:
  - `case_coverage_matrix`
  - `market_finance_matrix`
  - `prediction_market_matrix`
  - `multilingual_regional_context`
  - `theater_watch_summary` for SOCCENT, SOCEUR, SOCPAC, SOCAFRICA,
    SOCSOUTH, SOCKOR, and SOCOMD
  - `overflow_candidate_cases` when credible cases exceed the active packet
    limit
  - source relationships
  - source URLs and citations
  - source quality fields: `strong_sources`, `weak_sources`,
    `missing_source_lanes`, `cue_only_lanes`, and `next_collection_priority`
  - `commander_ready=false`
  - `mutation_performed=false`
- Emit up to five active candidate packets by default. Do not omit other
  theaters silently; record no-case, not-checked, blocked, stale, or overflow
  states explicitly.

If the output fails schema validation, AUTOSINT quarantines it and the Live
Case Board does not update from that capture.

Until Scheduled Tasks are proven over two natural output -> capture cycles, the
local Packet-chat prompt trigger remains fallback. Fallback trigger receipts
must prove exact Packet-chat target selection, request-id visibility in the
user turn, strict packet request-id match, `validation_error_count=0`, and a
fresh generated_at before capture promotes output. If a Scheduled Task cannot
be edited to write into the canonical Packet chat, stop and request approval
before replacing it or creating a duplicate.

Current status as of 2026-06-28: Scheduled Tasks are configured but not
production-primary. The existing `AUTOSINT Daily External Scout` task was
updated with the strict self-contained prompt and resumed, but its proof run
stayed visible as `Выполняется` for more than ten minutes, did not expose a
run-now/result-chat control, and did not advance the Packet chat before the
natural capture. The Packet-chat local prompt trigger remains the working
production upstream until a stable Scheduled Task output conversation is
identified and two natural cycles are proven. When a task-result chat is found,
validate it with the scheduled-task probe first; do not repoint the production
Packet capture target until the task output is strict-valid and newer than the
inbox. Outside-project `chatgpt.com/c/...` task result chats are not production
targets for AUTOSINT; production proof must remain inside the AUTOSINT External
Scout Project or the canonical Project Packet chat. The current live task is
paused after the outside-project result-chat test; keep it paused until a
Project-scoped Scheduled Task output path is available.

### AUTOSINT System Control

`AUTOSINT System Control` is the human/admin chat.

Purpose:

- Codex task handoff.
- GitHub and context mirror work.
- launchd and capture operations.
- Prompt updates.
- Architecture review.
- Debugging.
- Roadmap and cleanup planning.

This is where the user discusses system changes. It can reference the public
context mirror, but repo/runtime evidence remains authoritative.

### CASE - <topic>

`CASE - <topic>` chats are optional human-created deep-dive chats.

Use them only for important analyst deep dives. Do not auto-create one per
packet, one per thread, or one per hourly capture.

A case deep-dive chat must start from AUTOSINT thread data:

- `thread_id`
- `topic_key`
- latest `generated_at`
- current BLUF
- what changed since the previous capture
- source gaps
- coverage matrix
- decision
- the user's specific question

A case deep-dive chat is not source of truth. Any useful output must be
translated back into AUTOSINT as candidate notes or future approved workflow
input. It must not be treated as Evidence.

## Do-Not-Do Rules

- Do not put manual discussion into `AUTOSINT Daily External Scout`.
- Do not let ChatGPT chats become the case database.
- Do not depend on Project files for scheduled task execution.
- Do not create one chat per hourly packet.
- Do not create one chat per thread automatically.
- Do not treat ChatGPT output as Evidence.
- Do not treat ChatGPT safety flags as authoritative.
- Do not use ChatGPT Project state as a substitute for AUTOSINT validation,
  quality gates, quarantine, OSIR policy, or future explicit approval.

## Source Of Truth

AUTOSINT source-of-truth surfaces:

- Case memory: `/external-scout/threads`
- Packet inbox: `/external-scout`
- Operator package: `/havoc-rfi/SOCCENT`
- Durable public context: `tg-osint-eucom/autosint-context`
- Private code/runtime: `tg-osint-eucom/autosint`

ChatGPT Project chats are workspaces around those surfaces.

## When To Create A Case Deep-Dive Chat

Create an optional `CASE - <topic>` chat only when at least one of these is
true:

- A thread is Escalating.
- The user wants manual analysis.
- A HAVOC/RFI package needs human review.
- A PIR question needs exploration.
- A source conflict needs deeper reasoning.

Do not create case deep-dive chats for routine hourly updates.

## Case Deep-Dive First Message Template

Use this template when creating a human deep-dive chat:

```text
This is a human-created AUTOSINT case deep dive. AUTOSINT Live Case Board is
the source of truth. This chat is not Evidence, not case-linking, not OSIR,
and not commander-ready.

thread_id:
topic_key:
latest generated_at:
current BLUF:
what changed since previous capture:
source gaps:
market/prediction status:
multilingual/regional status:
decision:
question to analyze:
```

## Context Restore

When ChatGPT/Codex context is lost, restore from the public sanitized context
mirror:

- https://raw.githubusercontent.com/tg-osint-eucom/autosint-context/main/docs/status/AUTOSINT_CONTEXT_INDEX.md
- https://raw.githubusercontent.com/tg-osint-eucom/autosint-context/main/docs/status/AUTOSINT_ASSISTANT_CONTEXT_CURRENT.md

The public context mirror is sanitized and does not contain code secrets, DB
files, External Scout runtime artifacts, raw Evidence, browser state, cookies,
tokens, or private session data.

Codex memories may be enabled for helper recall, but they are not project
source of truth. Durable operating rules must be in `AGENTS.md` or tracked
AUTOSINT docs, and current thread context is temporary working context only.

Recommended Codex memory setting:

```toml
[features]
memories = true
```

Use `/goal` for substantial AUTOSINT work so objectives and verification gates
remain explicit. After meaningful commits, refresh the public
`autosint-context` mirror so ChatGPT/Codex can restore current project context
from tracked, sanitized docs.

## Safety Boundary

This operating model does not authorize:

- DB mutation.
- Raw Evidence mutation.
- Case-link mutation.
- Source-config mutation.
- OSIR bypass.
- Apply/import path.
- Commander-ready promotion.
- Frontend write controls.
- Reading cookies, sessions, browser storage, Chrome profile files, tokens,
  credential files, `.env` values, or private browser state.
