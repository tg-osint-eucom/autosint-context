# AUTOSINT External Scout Runbook

- Status: Current
- Authority: Canonical runbook
- Owner: External Scout
- Last reviewed: 2026-07-16
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
4. Binds the prompt to the configured target, root request, generation attempt,
   attempt number, contract version, and contract SHA.
5. Requests 1-3 current cases by default, never more than the configured
   absolute maximum of 5.
6. Requests all seven theater rows and all 19 operational lane rows.
7. Writes a sanitized prompt receipt and pending metadata.

Cycle-level `source_checks`, `market_checks`, `prediction_market_checks`, and
`multilingual_checks` bind only to the first primary finding. Secondary
findings carry their own rows; the normalizer does not copy primary-case
metrics into them.

Required cycle identity fields are:

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

Every cycle accounts for:

- seven theaters: `SOCCENT`, `SOCEUR`, `SOCPAC`, `SOCAFRICA`, `SOCSOUTH`,
  `SOCKOR`, and `SOCOMD`;
- all 19 operational source lanes from the system contract;
- prediction rows `polymarket`, `kalshi`, and
  `other_prediction_markets` (Manifold / Other Prediction Markets);
- market/finance rows `broad_market`, `oil_energy`, `shipping_tanker`,
  `insurance_freight_rates`, `defense_large_cap`, `defense_mid_small`,
  `regional_market`, and `crypto_risk`.

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
3. Requires matching `system_contract_version`, root request, generation
   attempt id, and attempt number.
4. Requires output newer than the prompt and newer than the active inbox.
5. Accepts the primary inline transport or the fallback attachment transport,
   never two competing full payloads.
6. Normalizes matching Scout Findings into strict candidate packets.
7. Applies structural, semantic, and preservation gates.
8. Promotes only if every gate passes; otherwise it skips or quarantines and
   leaves active state unchanged.

Promotion requires:

```text
structural_validation_error_count=0
semantic_validation_error_count=0
preservation_error_count=0
normalizer_run=true
promoted_to_inbox=true
```

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
single new natural cycle may accept a runtime code change but does not replace
the canonical 3/3 proof gate.

Do not merge fields from receipts with different timestamps. Report the latest
prompt, harvest, promotion, thread, health, and proof snapshots separately when
they differ.

## Failure Classification

Classify the exact receipt-backed failure before taking action:

- contract guard RED;
- duplicate blocked by pending request;
- target or request/attempt mismatch;
- output predates prompt or active inbox;
- active without observed progress;
- stopped, stalled, or expired generation;
- transport mismatch or duplicate full payloads;
- normalization failure;
- structural validation failure;
- semantic validation failure;
- preservation failure;
- promotion freshness failure;
- stale board, zero active threads, health RED, or eval hard-fail.

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
