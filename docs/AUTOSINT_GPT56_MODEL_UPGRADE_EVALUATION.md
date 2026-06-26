# AUTOSINT GPT-5.6 Model Upgrade Evaluation

## BLUF

GPT-5.6 model-family adoption is an evaluation workstream only. AUTOSINT does
not replace its current prompt, capture, validation, Live Case Board, or
HAVOC/RFI loop until availability, replay quality, latency, cost, and safety
gates are proven in non-production evaluation.

Current official source checked:

- <https://openai.com/index/previewing-gpt-5-6-sol/>

Treat public model announcements as product input, not AUTOSINT runtime truth.
Before any migration, verify actual access in the relevant surface:

- ChatGPT Project model picker, if used manually.
- Codex model availability, if used for development tasks.
- API model availability, if used for scripted evaluation.

Do not read or print API keys, tokens, `.env` values, browser cookies, browser
storage, Chrome profile files, credentials, or private browser state during
availability checks.

## Candidate Model Roles

### Sol

Use Sol, if available, only for high-difficulty reasoning and review tasks:

- hard Codex implementation goals;
- root-cause debugging across prompts, capture receipts, thread reports, tests,
  and route output;
- deep operator-page review;
- architecture and safety-gate review;
- adversarial review of packet/schema drift.

Sol should not be the default hourly packet-generation model without a separate
cost, latency, and reliability proof.

### Terra

Use Terra, if available, as the first candidate for routine AUTOSINT work:

- External Scout prompt-quality evaluation;
- non-production packet replay;
- thread and HAVOC/RFI preview review;
- routine source-gap summaries;
- workstream status synthesis.

Terra may become the preferred routine model only after replay tests show it
preserves strict packet schema, coverage matrices, cue-only language, and
read-only safety boundaries.

### Luna

Use Luna, if available, only for low-risk helper tasks:

- short summaries;
- diff summaries;
- checklist expansion;
- log/receipt triage;
- low-cost smoke review.

Luna output must not drive packet promotion, thread-current selection, HAVOC/RFI
readiness, OSIR, Evidence, case links, source config, apply/import, or
commander-ready status.

## Non-Production Evaluation Gates

### 1. Availability Inventory

Record what is actually available on this host and account:

- ChatGPT Project availability.
- Codex availability.
- API availability.
- access limitations, preview restrictions, rate limits, or missing surfaces.

Do not use secrets or private browser state to prove availability. If an API
check requires credentials, stop and ask for explicit approval for the exact
credential flow.

### 2. Offline Replay

Run model candidates only against sanitized, ignored, non-production inputs:

- previous operator page dumps;
- sanitized thread report snapshots;
- sanitized HAVOC/RFI preview payloads;
- tracked docs;
- generated evaluation prompts that do not contain secrets, DB rows, raw
  Evidence bodies, browser state, or source catalog content.

No replay output may write to External Scout inbox, staging, quarantine, latest,
DB, Evidence, case links, source config, OSIR, apply/import, launchd, or
commander-ready state.

### 3. Strict Packet Contract Replay

For any candidate model used to generate External Scout-style output, evaluate
against the current strict packet requirements:

- `candidate_packets` top-level object;
- `case_coverage_matrix`;
- `market_finance_matrix`;
- `prediction_market_matrix`;
- `multilingual_regional_context`;
- `source_relationships`;
- `source_urls`;
- `citations`;
- `theater_watch_summary`;
- `overflow_candidate_cases` when relevant;
- cue-only caveats for markets, prediction markets, crypto, social, and public
  comments;
- `commander_ready=false`;
- `mutation_performed=false`.

The validator and thread report remain authoritative. A model is not accepted
because it sounds better; it is accepted only if it validates and improves or
preserves operator usefulness.

### 4. Live Case Board And HAVOC/RFI Replay

Evaluate whether outputs preserve current operator behavior:

- active threads remain readable;
- stale and archived threads remain separated;
- source checks and follow-up gaps remain explicit;
- market/prediction/finance lanes remain explicit and cue-only;
- HAVOC/RFI uses thread-current state;
- commander-ready remains `false`;
- OSIR remains closed;
- no Evidence/case-link/source-config/apply/import path is introduced.

### 5. Cost, Latency, And Reliability

Record:

- average generation latency;
- timeout/failure behavior;
- validator pass rate;
- missing-lane rate;
- quality regressions;
- cost if available;
- whether the model is stable enough for scheduled or repeated use.

Do not promote a model into the hourly production loop solely because a single
manual response looks good.

## Stop Conditions

Stop evaluation and do not migrate if any candidate:

- is unavailable in the intended surface;
- requires reading secrets or private browser state;
- produces invalid strict packets;
- omits required theater, source, market, prediction, finance, or multilingual
  lanes silently;
- treats cue-only market/social/prediction material as proof;
- marks `commander_ready=true`;
- implies OSIR release, Evidence creation, case-linking, source-config mutation,
  apply/import, or other write behavior;
- increases stale/wrong-chat/capture failures;
- cannot be evaluated without committing generated artifacts.

## Evaluation Artifacts

Generated evaluation artifacts must remain ignored under `artifacts/`, for
example:

```text
artifacts/model_eval/gpt56/latest/
```

Tracked docs may summarize sanitized findings, but must not include secrets,
private browser state, DB rows, raw Evidence bodies, capture inbox payloads, or
source catalog content unless separately approved.

## Required Outcome Before Any Migration

Before changing production prompts, capture behavior, model defaults, or
scheduled workflows, produce a tracked or ignored evaluation report that states:

- model availability by surface;
- replay input set;
- validator pass/fail counts;
- route/report impact;
- latency/cost notes;
- exact recommended role for each model;
- whether migration is recommended;
- why migration is not yet approved, if applicable;
- safety confirmations.

Default decision until proven otherwise: no production migration.
