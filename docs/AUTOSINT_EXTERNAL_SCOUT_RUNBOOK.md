# AUTOSINT External Scout Runbook

- Status: Current
- Authority: Canonical runbook
- Version: 2.1
- Owner: External Scout
- Last reviewed: 2026-07-18
- Runtime truth: Only when paired with current receipts and canonical reports
- Supersedes: Direct-capture scheduling, direct-packet default, and embedded incident transcripts
- Superseded by: None
- Related: [System Contract](status/AUTOSINT_SYSTEM_CONTRACT_CURRENT.md), [Project Operating Model](AUTOSINT_CHATGPT_PROJECT_OPERATING_MODEL.md), [Primary Workflow](AUTOSINT_PRIMARY_WORKFLOW.md)

This runbook defines the current production procedure only. Dated incidents and
recovery experiments remain in Git history or ignored operator artifacts; they
do not define the current contract.

## Authority And Safety

The cross-cutting machine authority is
`config/autosint_system_contract.yml`. Its generated review view is
`docs/status/AUTOSINT_SYSTEM_CONTRACT_CURRENT.md`.

External Scout output is candidate input only. This runbook does not authorize:

- DB or raw Evidence mutation;
- case-link or source-config mutation;
- OSIR, apply/import, or commander-ready promotion;
- manual browser-private-state inspection;
- manual prompt, harvester, capture, recovery, or launchd mutation unless a
  separate current task explicitly authorizes the exact action.

## Production Schedule

The normal local production path is:

```text
:00 scheduled prompt trigger
-> configured Packet chat emits Scout Findings
-> exact pending request/attempt remains authoritative
-> :28 scheduled async harvester
-> deterministic normalization and validation
-> promotion or fail-closed receipt
-> packet refresh, Threads, proof, health, and /external-scout/24-7
```

Direct capture is manual diagnostic/emergency tooling only. It is not part of
the scheduled production proof loop and never counts toward natural proof.

## Preflight Contract Guard

The deterministic Contract Guard runs before prompt or harvester browser
action. It checks the versioned producer, transport, lifecycle, case, theater,
lane, status, proof, model-policy, route, and required-semantic-row contract.

- `GREEN`: contract checks passed.
- `WARN`: runtime may proceed; warning remains visible.
- `RED`: prompt and harvester fail closed before browser action.

A blocked receipt records:

- `contract_guard_blocked=true`
- `conflict_codes`
- `system_contract_version`
- `system_contract_sha256`
- `browser_action_performed=false`

The read-only API and AUTOSINT.app remain available under contract RED and show
`CONTRACT_CONFLICT_RED`.

## Producer And Transport

Canonical producer mode:

```text
scout_findings_normalized
```

ChatGPT emits Scout Findings. AUTOSINT deterministically normalizes them into
strict candidate packets. Direct `candidate_packets` is fallback/replay only,
not a simultaneous production default.

Transport contract:

1. Primary: `inline_fenced_json` with one complete fenced JSON object.
2. Fallback: `downloadable_json_attachment` only when inline output cannot be
   produced.
3. Never emit both full payloads.

The harvester supports both transports but accepts neither without exact
request and attempt identity.

## Prompt Window

The scheduled prompt actor:

1. Loads the canonical system contract.
2. Runs the Contract Guard before any browser action.
3. Refuses a duplicate when a non-terminal exact pending request exists.
4. Records the loader-selected contract as `expected_system_contract_*`, then
   binds the pending request to that exact receipt identity as
   `bound_system_contract_*`, together with the configured target hash, root
   request, generation attempt, and attempt number.
5. Requests 1-3 current cases by default, never more than the configured
   absolute maximum of 5.
6. Requests `GLOBAL_THEATER_SWEEP`, exactly seven real bounded theater rows,
   one mandatory oldest-due deep dive, a distinct priority deep dive when
   available, and an optional severe third slot. The full 19-lane matrix is
   required for emitted cases; non-emitted theater rows use compact source
   family accounting.
7. Writes a sanitized prompt receipt and pending metadata.

Cycle-level `source_checks`, `market_checks`, `prediction_market_checks`, and
`multilingual_checks` bind only to the first primary finding. Secondary
findings carry their own rows; the normalizer does not copy primary-case
metrics into them. Under `autosint-system-contract-v2.1`, top-level
`theater_source_checks` is separate cycle-scoped theater evidence and never
inherits that primary-case binding.

The four contract identity roles are explicit. Expected, bound, and validation
identity values are machine-owned; the reported values are model-originated
diagnostic metadata:

- `expected_system_contract_*`: selected by the AUTOSINT loader and recorded
  in the prompt receipt.
- `bound_system_contract_*`: copied by AUTOSINT from the prompt receipt into
  pending and harvest state.
- `reported_system_contract_*`: copied from model output for diagnostics only.
- `validation_system_contract_*`: selected by AUTOSINT from `bound_*` and used
  for schema, validator, normalizer, promotion, and proof decisions.

Legacy `system_contract_*` fields remain validation aliases for historical
receipts and replay fixtures. They do not give the model authority to select a
validator. Required cycle identity and policy fields are:

- `system_contract_version`
- `system_contract_sha256`
- `producer_mode`
- `requested_output_transport`
- `default_case_policy`
- `model_policy_required_label`
- `model_selection_status`
- `trigger_request_id`
- `generation_attempt_id`
- `generation_attempt_number`

The required Project model is operator-confirmed policy. It is not attributed
to a cycle without an approved receipt field.

## Pending Lifecycle And Busy State

One exact pending request owns the generation lifecycle. Page-global busy state
without exact attempt ownership is ambiguous and fails closed.

It must not:

- authorize a second submit;
- clear or replace the pending request;
- create a replacement conversation/root;
- count as `response_start_confirmed`;
- count as useful generation progress.

Progress is attempt-bound. Distinguish:

- active with observed progress;
- active without observed progress;
- stalled;
- stopped without output;
- expired;
- mismatched output.

A visible Stop control alone proves none of these states.

## Scout Findings Requirements

Natural output contains 1-3 current cases by default and no more than 5.
Explicit bounded recovery, when separately approved, requests exactly 1 case.

Natural output uses `cycle_scope=GLOBAL_THEATER_SWEEP`. It has exactly one row
for each canonical theater and never uses `Not checked` as a placeholder.
Recovery output uses `cycle_scope=FOCUSED_THEATER_DEEP_DIVE`, one honest theater
row, `recovery_assisted=true`, and `natural_cycle_eligible=false`.

Every cycle accounts for:

- seven theaters: `SOCCENT`, `SOCEUR`, `SOCPAC`, `SOCAFRICA`, `SOCSOUTH`,
  `SOCKOR`, and `SOCOMD`;
- all 19 operational source lanes from the system contract;
- prediction rows `polymarket`, `kalshi`, and
  `other_prediction_markets` (Manifold / Other Prediction Markets);
- market/finance rows `broad_market`, `oil_energy`, `shipping_tanker`,
  `insurance_freight_rates`, `defense_large_cap`, `defense_mid_small`,
  `regional_market`, and `crypto_risk`.

Every global theater row includes `theater`, `checked`, `sweep_status`,
`window_start`, `window_end`, `active_case_found`, `emitted_packet_id`,
`top_candidate_topic`, `top_watched_topics`, `candidate_count`,
`source_families_checked`, `family_results`, `coverage_gaps`,
`deep_dive_recommended`, and
`next_check`. Missing, duplicate, or unknown theater rows fail closed. An
explicit `Not checked` row is visible incomplete coverage and requires a gap
reason plus next check.

Every `family_results` array contains exactly one result for each configured
minimum family: `Official / Advisory`, `Public News`, and
`Multilingual / Regional`. Its `evidence_refs` values must resolve to
`source_check_id` rows from top-level `theater_source_checks`. Every evidence
reference must resolve within the same output, theater, and source family. Only
evidence references credited to `Checked and found` or `Checked and not found`
completion must be current-window. Stale and candidate follow-up references
are allowed, remain incomplete, and never receive completion credit.

Exact `check_method` values are `bounded_official_advisory_review`,
`bounded_public_news_review`, `bounded_multilingual_regional_review`,
`approved_read_only_adapter`, and `not_checked`. Exact `public_access_mode`
values are `public_no_login`, `approved_read_only_adapter`,
`blocked_login_or_license`, `candidate_only`, and `not_checked`. Generic prose
in `check_method`, candidate URLs, and HTTP availability never prove coverage.
An adapter row remains `GATED_DISABLED` unless `adapter_result_ref` resolves to
a trusted current AUTOSINT runtime record.

Machine-owned `source_check_completion_basis_by_primary_status` supplies the
exact mapping. Every V2.1 check has `completion_basis`: `substantive_content` pairs only
with `Checked and found`, `bounded_no_result` only with `Checked and not
found`, and `none` only with candidate, blocked, stale, or not-checked states.
Any mismatch is a hard validation error, not a downgrade. Source-check
`result_summary` and `check_method_note` are informational only. Opaque
`source_check_id` and `evidence_refs` values match
`^[A-Za-z0-9][A-Za-z0-9:_-]{0,95}$`; URLs and token-shaped values are invalid
IDs.

`Checked and found` completes only with `completion_basis=substantive_content`
and qualifying current referenced evidence. `Checked and not found` completes
only with `completion_basis=bounded_no_result`, a referenced bounded
current-window attempt, a safe public itinerary URL or trusted adapter result,
and zero validated found sources. Its family result must set
`checked_not_found=true` and contain `no credible current result was found`;
the phrase alone is only a consistency requirement. AUTOSINT
derives canonical primary and coverage status, checked, validated, candidate,
blocked, and stale counts, currentness, and theater completion. Candidate,
blocked, stale, and not-checked results remain honest incomplete follow-ups and
never count as proof or downgrade a completed primary.

Every performed deep-dive slot includes theater, selection reason, checked
source families, and a global event key. Every emitted case includes one stable
`global_event_key`, one primary theater, supporting theater references,
duplicate lineage, and a cross-theater reason. Repeated event keys fail closed;
supporting references do not create additional active threads.

Required semantic row fields:

- `status`
- `summary`
- `source_urls`
- `metrics`
- `what_it_suggests`
- `what_it_does_not_prove`
- `collection_gap`
- `next_check`
- `cue_only`

Allowed source statuses are defined by the system contract. A generated
`Not checked` row is structural accounting with `collection_complete=false`;
it does not prove collection. Candidate URLs are not imported and do not close
a lane. Cue-only rows are never proof-capable.

## Async Harvester Window

The scheduled harvester:

1. Loads the same system contract and runs the guard before browser action.
2. Requires the exact configured target and pending request.
3. Before browser access, requires prompt `expected_*` to match pending
   `bound_*`, requires the bound contract to be loadable, and requires matching
   target hash, root request, generation attempt id, and attempt number.
4. Requires output newer than the prompt and newer than the active inbox.
5. Accepts the primary inline transport or the fallback attachment transport,
   never two competing full payloads.
6. Normalizes matching Scout Findings into strict candidate packets.
7. Applies structural, semantic, and preservation gates.
8. Promotes only if every gate passes; otherwise it skips or quarantines and
   leaves active state unchanged.

The model-reported contract identity remains required by the producer output
policy, but its value or absence never selects validation authority. The
harvester preserves the reported value or explicit missing state and classifies
it as `MATCH`, `MISMATCH`, `MISSING_VERSION`, `MISSING_SHA`, `MISSING_BOTH`, or
`MALFORMED`. `reported_identity_severity` is `INFO` for `MATCH` and `WARN` for
every other state; `reported_contract_identity_severity` remains a compatibility
alias. Every state is `diagnostic_only=true`. No reported-identity state
independently blocks normalization, promotion, proof eligibility, or rotation
when the complete machine-owned identity chain and every substantive gate pass.
AUTOSINT continues with
`validation_system_contract_* = bound_system_contract_*`; it never backfills a
missing reported value from the bound value.

Promotion requires:

```text
structural_validation_error_count=0
semantic_validation_error_count=0
preservation_error_count=0
global_coverage_validation_error_count=0
theater_semantic_error_count=0
cross_theater_duplicate_count=0
theater_source_check_validation_error_count=0
theater_closure_validation_error_count=0
candidate_as_coverage_error_count=0
machine_contract_identity_error_count=0
normalizer_run=true
promoted_to_inbox=true
```

`minimum_family_gap_count` may remain nonzero only for valid honest incomplete
coverage. It is not a promotion gate by itself; it prevents theater completion
and therefore prevents rotation credit, but a structurally and semantically
valid packet may still promote and refresh current state. A missing or malformed
required family also increments `theater_closure_validation_error_count` and
fails closed.

Schema-clean output is insufficient when required semantic rows or provider
notes were dropped.

## Preservation Guard

`scripts/check_external_scout_preservation.py` traces:

```text
raw Scout Findings
-> normalized packet
-> thread state
-> proof/API
-> UI/RFI
```

It checks aggregate source checks, market metrics, prediction summaries,
`provider_status_notes`, row-level `cue_only`,
`insurance_freight_rates`, and Manifold semantics. Promotion fails closed on a
preservation error.

## Proof And Health

The single operator page is `/external-scout/24-7`. The matching machine source
is `/api/v1/external-scout/24-7-proof`.

Read-only checks:

```bash
PYTHONPATH=src:. .venv/bin/python -m autosint_external_scout_capture.cli --status
.venv/bin/python scripts/report_external_scout_threads.py --dry-run
.venv/bin/python scripts/monitor_external_scout_health.py --once
.venv/bin/python scripts/check_autosint_ui_host_status.py --once
.venv/bin/python scripts/report_external_scout_24_7_proof.py --dry-run
```

`PROVEN` requires three consecutive eligible natural cycles, Live Board
`stale=false`, active threads greater than zero, no RED health, and no eval
runtime hard-fail. A manual or recovery-assisted cycle does not count. A
single receipt-backed naturally scheduled `autosint-system-contract-v2.1`
cycle may establish natural acceptance of the typed contract, but it does not
replace or imply the canonical 3/3 proof gate. Until such a cycle is observed,
report V2.1 natural acceptance as not yet proven.

Global theater coverage and deep-dive rotation are separate from canonical
runtime reliability proof. `PROVEN 3/3` does not mean seven theaters were
checked. Explicit `Not checked`, `Stale`, or blocked rows may produce coverage
WARN while a receipt-clean natural cycle remains proof eligible. Missing rows,
semantic row errors, or cross-theater duplicates block promotion.

Do not merge fields from receipts with different timestamps. Report the latest
prompt, harvest, promotion, thread, health, and proof snapshots separately when
they differ.

## Failure Classification

Classify the exact receipt-backed failure before taking action:

- contract guard RED;
- prompt expected versus pending bound contract mismatch;
- missing or unsupported machine-bound contract identity;
- duplicate blocked by pending request;
- target or request/attempt mismatch;
- output predates prompt or active inbox;
- active without observed progress;
- stopped, stalled, or expired generation;
- transport mismatch or duplicate full payloads;
- model-reported contract identity `MATCH` (diagnostic INFO), or mismatch,
  missing, and malformed states (diagnostic WARN only);
- normalization failure;
- structural validation failure;
- semantic validation failure;
- preservation failure;
- promotion freshness failure;
- stale board, zero active threads, health RED, or eval hard-fail.

V2.3 diagnostic-only handling applies only to new cycles processed by the
current V2.3 runtime. A receipt that terminally failed before V2.3 remains
`failed`: AUTOSINT does not retroactively reclassify it, grant V2.3
implementation acceptance or natural proof credit, advance rotation, or create
a promotion after the fact. Any historical replay, if one is ever explicitly
authorized, must be separately labeled as replay and must not alter production
proof history.

Do not loop blindly. Scheduled actors own pending output. Recovery requires an
explicit current authorization and never counts as natural proof.

## RFI And Thread Consumers

- `/external-scout/threads` owns durable thread-current state.
- `/rfi` renders the read-only workspace/theater overview.
- `/rfi/{workspace}` renders the read-only selected-thread/case preview.

RFI consumes thread-current state first and validator-clean packet fallback
only when thread-current is unavailable. It remains analyst-review-only,
candidate-input-only, not Evidence, not OSIR, not apply/import, and not
commander-ready.

## Project Instructions

Generate the canonical manual-sync template with:

```bash
.venv/bin/python scripts/render_autosint_system_contract.py --write
```

Verify an exact operator-supplied saved copy without inspecting private account
or browser state:

```bash
.venv/bin/python scripts/verify_external_scout_project_instructions.py /path/to/operator-copy.txt
```

Until exact comparison passes, report `NOT_VERIFIED_OPERATOR_SETTING`.
