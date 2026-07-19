# AUTOSINT ChatGPT Project Operating Model

- Status: Current
- Authority: Canonical workflow
- Owner: External Scout
- Last reviewed: 2026-07-18
- Runtime truth: No; current cycles require receipts and the proof reporter
- Supersedes: Direct strict-packet default and Scheduled Task incident narratives
- Superseded by: None
- Related: [System Contract](status/AUTOSINT_SYSTEM_CONTRACT_CURRENT.md), [External Scout Runbook](AUTOSINT_EXTERNAL_SCOUT_RUNBOOK.md)

The ChatGPT Project named `AUTOSINT External Scout` is a workspace. AUTOSINT
threads are durable case memory and AUTOSINT remains authoritative for active
state.

```text
AUTOSINT threads are case memory. ChatGPT chats are workspaces.
```

ChatGPT output is candidate input only. It is not Evidence, OSIR, a case link,
an apply/import action, or commander-ready intelligence.

## Canonical Production Contract

Cross-cutting values come from
`config/autosint_system_contract.yml` and its generated human-readable view,
`docs/status/AUTOSINT_SYSTEM_CONTRACT_CURRENT.md`.

The production sequence is:

```text
configured Packet chat
-> Scout Findings
-> exact request/attempt binding
-> scheduled async harvester
-> deterministic strict-packet normalization
-> structural, semantic, and preservation validation
-> inbox promotion when every gate passes
-> thread-current and Live Case Board
```

Producer and consumer roles are distinct:

- ChatGPT produces Scout Findings in the default production mode
  `scout_findings_normalized`.
- AUTOSINT normalizes Scout Findings into strict candidate packets.
- Direct `candidate_packets` is an explicit fallback/replay mode only.
- The two producer modes are never active simultaneously.

## Output Transport

The transport contract is `autosint_scout_findings_transport_v1`:

1. Primary: one complete fenced JSON object in the assistant turn with
   `transport=inline_fenced_json`.
2. Fallback: one downloadable JSON attachment only when the primary inline
   payload cannot be produced.
3. Never emit both full payloads in one response.

The harvester may validate either transport, but only when it matches the exact
pending request and generation attempt. A filename or visible page state alone
does not establish identity.

Every output includes:

- `system_contract_version`
- `system_contract_sha256`
- `trigger_request_id`
- `generation_attempt_id`
- `generation_attempt_number`

These remain required producer fields, but AUTOSINT does not grant them
validation authority. A present, mismatching, missing, or malformed
model-reported contract identity is preserved as diagnostic metadata only.
The machine-owned expected, bound, and validation chain selects schema,
normalizer, validator, promotion, proof, and rotation authority; all substantive
gates remain fail closed.

## Case, Theater, And Source Accounting

- Natural response: 1-3 current cases by default.
- Absolute maximum: 5 cases.
- Explicit bounded recovery: exactly 1 case.
- Normal natural cycles use `GLOBAL_THEATER_SWEEP` and account for all seven
  configured theaters with exactly one real bounded row each. Explicit bounded
  recovery uses `FOCUSED_THEATER_DEEP_DIVE`, one theater row, and is not global
  coverage or proof eligible.
- Each successful complete global cycle performs the mandatory oldest-due
  rotation deep dive, a distinct priority deep dive when available, and at
  most one severe-event deep dive. Failed, incomplete, manual, or
  recovery-assisted cycles do not advance rotation.
- Cross-theater events use one primary case/thread and supporting theater
  references. Korea uses `SOCKOR` primary with `SOCPAC` support; `SOCOMD` is
  command rollup unless an event is genuinely command-wide.
- All 19 configured operational lanes are accounted for every cycle.
- `Manifold / Other Prediction Markets` and
  `insurance_freight_rates` are required first-class rows.

`Not checked`, `Stale`, and `Blocked / login required` are honest states. A
normalizer-generated `Not checked` row provides structural accounting but does
not prove that collection occurred or that the lane is complete.

Under `autosint-system-contract-v2.1`, top-level `theater_source_checks` is
cycle-scoped theater evidence. It is separate from the primary-case
`source_checks` collection. Every theater row returns `family_results` with
exactly one result for each configured minimum family: `Official / Advisory`,
`Public News`, and `Multilingual / Regional`.

`check_method` uses only `bounded_official_advisory_review`,
`bounded_public_news_review`, `bounded_multilingual_regional_review`,
`approved_read_only_adapter`, or `not_checked`. `public_access_mode` uses only
`public_no_login`, `approved_read_only_adapter`,
`blocked_login_or_license`, `candidate_only`, or `not_checked`. Generic prose
belongs only in optional `check_method_note` and never proves a check.

Machine-owned `source_check_completion_basis_by_primary_status` supplies the
exact status pairing. Every V2.1 source-check row also has `completion_basis`
value
`substantive_content`, `bounded_no_result`, or `none`. The first pairs only
with `Checked and found`, the second only with `Checked and not found`, and
`none` only with candidate, blocked, stale, or not-checked states. A mismatch
is a hard validation error, never a downgrade. Source-check `result_summary`
and `check_method_note` are informational only. Opaque `source_check_id` and
`evidence_refs` values must match `^[A-Za-z0-9][A-Za-z0-9:_-]{0,95}$`; URLs,
JWTs, signed strings, and IDs containing `/`, `.`, `?`, `=`, or `@` are
invalid.

Each family result reports `reported_primary_status`,
`reported_coverage_status`, and `evidence_refs`. Every evidence reference must
resolve within the same output, theater, and source family. Only evidence
references credited to `Checked and found` or `Checked and not found`
completion must be current-window. Stale and candidate follow-up references
are allowed, remain incomplete, and never receive completion credit. AUTOSINT
derives canonical status, checked, validated, candidate, blocked, and stale
counts, plus theater completion; assistant-reported values are not authoritative.

`Checked and found` requires `completion_basis=substantive_content` and
qualifying current referenced evidence. `Checked and not found` requires
`completion_basis=bounded_no_result`, a referenced bounded current-window
attempt, zero validated found sources, and a safe public itinerary URL or
trusted adapter result. Its family result must also set
`checked_not_found=true` and contain `no credible current result was found`;
that phrase alone never proves completion. Candidate URLs,
HTTP availability, snippets, titles, blocked pages, and generic prose never
close a family. An `approved_read_only_adapter` row completes only when its
`adapter_result_ref` resolves to a trusted current AUTOSINT runtime record;
otherwise that path is `GATED_DISABLED` and incomplete.

Structurally and semantically valid honest incomplete coverage may promote and
refresh current state, but it cannot claim theater completion or rotation
credit. One receipt-backed naturally scheduled V2.1 acceptance establishes
contract acceptance only; canonical `PROVEN` still requires three consecutive
eligible natural cycles under the proof reporter. This document claims neither
current acceptance nor current proof.

## Required Project Model Policy

- Required label: `GPT-5.6 Sol Pro`.
- Policy status: `OPERATOR_CONFIRMED_REQUIRED_MODEL`.
- Selection status: `OPERATOR_CONFIRMED`.
- Account-setting machine verification: `NOT_PERFORMED`.
- Cycle attribution: `RECEIPT_REQUIRED`.
- API model id: `NOT_INFERRED`.

The operator-confirmed Project selection is a policy input, not independent
machine verification. AUTOSINT does not inspect private account state, model
pickers, cookies, sessions, browser storage, or credentials. A cycle is not
attributed to the required model unless an approved receipt field proves it.
The Project selection does not change an API model default.

## Project Instruction Sync

The tracked canonical template is generated from the system contract:

```text
docs/templates/EXTERNAL_SCOUT_PROJECT_INSTRUCTIONS_CANONICAL.txt
```

Codex does not edit private Project settings. The operator may paste that
template manually, copy the saved text back into an operator-supplied local
text file, and compare it with
`scripts/verify_external_scout_project_instructions.py`. Until that exact
comparison passes, the setting remains `NOT_VERIFIED_OPERATOR_SETTING`.

## Chat Roles

### Configured Packet Chat

The exact configured Packet chat is the machine-output workspace.

- Machine output only; no manual discussion.
- Do not ask follow-up questions.
- Emit the current contract payload only.
- Do not depend on Project files being available at runtime.
- Do not create a replacement chat while an exact pending request remains
  recoverable.

The local scheduled prompt trigger owns submission at the configured window.
The scheduled async harvester owns matching output. ChatGPT Scheduled Tasks are
not a second producer contract and are not production authority.

### AUTOSINT System Control

`AUTOSINT System Control` is the human/admin workspace for engineering tasks,
architecture review, runbook discussion, and sanitized handoffs. Repository
and receipt evidence remain authoritative.

### CASE - <topic>

Optional `CASE - <topic>` chats are human-created deep dives only. Do not
auto-create one per packet, case, thread, or cycle. Start from current AUTOSINT
thread data and return useful output only as candidate notes for a separately
approved workflow.

## Pending And Duplicate Discipline

Page-global busy state without exact attempt ownership is ambiguous and fails
closed. It must not:

- authorize a second submit;
- clear the current pending request;
- create a replacement root;
- count as response-start or useful generation progress.

Only exact request/attempt evidence may advance lifecycle state. Recovery
assistance never advances the natural-cycle proof streak.

## Source Of Truth

- Current proof and health: `/external-scout/24-7`
- Durable case memory: `/external-scout/threads`
- Validated packet inbox: `/external-scout`
- RFI overview: `/rfi`
- RFI workspace preview: `/rfi/{workspace}`

All are read-only operator/review surfaces under this contract.

## Safety Boundary

- No DB, raw Evidence, case-link, source-config, OSIR, apply/import, or
  commander-ready mutation.
- No browser-private-state inspection.
- No hidden model or API access inference.
- Market, prediction-market, crypto, social, and public-comment material is
  cue-only and cannot independently prove attribution, causality, or intent.
- `commander_ready=false` and `mutation_performed=false` remain required.
