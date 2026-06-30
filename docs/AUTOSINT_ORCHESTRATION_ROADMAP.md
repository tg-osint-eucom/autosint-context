# AUTOSINT Orchestration Roadmap

This roadmap records the next architecture layer for AUTOSINT without
committing the project to a migration. The current production loop remains the
local-first External Scout flow:

```text
:50 prompt trigger -> Packet chat strict output -> :08 capture -> validator ->
latest inbox -> Live Case Board -> HAVOC/RFI preview -> context mirror
```

## Current Verdict

Do not bring the full orchestration and agent-tooling stack into AUTOSINT at
once. The immediate need is observability over the proven local loop, not a
replacement of the loop.

Recommended staged path:

1. Native External Scout 24/7 proof reporter over local receipts and health.
2. Prefect spike for local workflow observability if the native report needs a
   run-history helper feeding the same `/external-scout/24-7` source.
3. LangGraph design later for controlled, read-only stateful agent loops.
4. LlamaIndex spike later for local knowledge retrieval over docs, receipts,
   page dumps, briefs, and context mirror files.
5. Keep AUTOSINT run observability inside the existing `/external-scout/24-7`
   page before considering external tracing/evaluation platforms.

Do not make Airflow, Dagster, CrewAI, AutoGen, n8n, LangSmith, or Arize the core
AUTOSINT loop right now.

## Current Evidence

As of the current inspection, AUTOSINT already has a working local control loop
with first-party proof artifacts:

- LaunchAgents for prompt trigger and capture.
- Prompt trigger receipts under ignored External Scout runtime artifacts.
- Capture receipts and capture logs.
- Strict validation status from the capture package CLI.
- External Scout thread reports.
- Live Case Board and HAVOC/RFI read-only routes.
- Workstream registry and status report.
- Sanitized public context mirror publishing.

Those receipts and status files are the first monitoring surface. Any new
orchestrator should read and summarize them before it tries to control them.

## Tool Positions

### Prefect

Use Prefect first as a small local/self-hosted orchestration observability
spike. Prefect is Python-native and designed to turn Python functions into
scheduled, monitored workflows with state tracking, retries, and run history.
That matches the current AUTOSINT shape: local Python scripts and package CLIs
with bounded receipts.

V1 spike scope:

- Wrap the existing prompt-trigger status command.
- Wrap the existing capture status command.
- Wrap thread report dry-run.
- Wrap context mirror dry-run.
- Summarize the last prompt/capture/thread state.
- Do not replace launchd.
- Do not perform DB, Evidence, case-link, source-config, OSIR, apply/import, or
  commander-ready mutations.

Success means a local operator can see recent run state and failure reasons in
one place. It does not mean Prefect owns scheduling yet.

### Airflow

Do not use Airflow first. Airflow is a strong batch-oriented platform for
developing, scheduling, and monitoring workflows, but it is heavier than the
current Mac-local prompt/capture loop and introduces more operational surface
than the immediate need requires.

Reconsider Airflow only if AUTOSINT later needs larger batch DAGs, separate
workers, larger external integrations, or organization-wide scheduling.

### Dagster

Do not use Dagster first. Dagster is attractive for asset-centric data products,
lineage, and materialization, but AUTOSINT's current blocker is operational
proof and local loop observability. It may become useful if External Scout
outputs, source coverage, case briefs, and HAVOC/RFI packages become formally
versioned data assets.

### LangGraph

Use LangGraph later for controlled stateful agent loops, not for capture
orchestration. Good future fits:

- PIR Hunter thread overlay.
- Source-gap hunter.
- Coverage completeness reviewer.
- Thread reviewer.
- HAVOC/RFI readiness reviewer.

Rules:

- Read-only agent state only.
- Agent outputs are candidate notes, not Evidence.
- No agent may write DB rows, Evidence, case links, source config, OSIR,
  apply/import state, commander-ready state, or browser-private state.
- Human/operator gates remain required.

Do not introduce CrewAI, AutoGen, or generic hidden LangChain chains as the core
AUTOSINT loop. AUTOSINT needs explicit state, receipts, and gates.

### LlamaIndex

Use LlamaIndex later for local retrieval and knowledge indexing, not for
capture orchestration. Good future corpus:

- Tracked docs.
- Public context mirror files.
- Operator page dumps.
- Source coverage exports.
- External Scout case briefs.
- HAVOC/RFI previews.
- Receipt summaries.

The first spike should be a local, sanitized read-only index over allowlisted
docs and generated review dumps. It must exclude DB dumps, raw Evidence bodies,
cookies, tokens, browser state, `.env` files, capture inbox payloads, and
anything private.

### n8n

n8n is not the AUTOSINT core orchestrator. It can be considered only for
low-risk notifications or manual review handoffs after the authoritative loop
is stable, and it must not become a second External Scout operator site.

n8n must not receive:

- DB write access.
- Evidence write access.
- Case-link write access.
- Source-config mutation access.
- OSIR/apply controls.
- Browser-private state.
- Tokens, `.env` values, cookies, or credentials.

### LangSmith

Do not add LangSmith until AUTOSINT has actual LangGraph/LangChain agent traces
or a stable evaluation dataset. If used later, it should trace only sanitized
agent decisions and evaluation metadata, not raw Evidence, private browser
state, source credentials, or sensitive runtime artifacts.

### Arize / Phoenix

Use existing receipts first. Consider Phoenix/Arize later if AUTOSINT needs
local/open-source LLM observability, evaluation runs, or retrieval/agent quality
reports with explicit redaction rules. Any operator-facing summary should feed
the existing `/external-scout/24-7` source instead of creating a parallel site.

## First Spike Proposal

Name: `orchestration_prefect_spike`

Goal: Build a read-only Prefect flow around the current local loop without
changing launchd ownership.

Flow outline:

```text
inspect prompt-trigger receipts
inspect capture receipts
run capture status
run thread report dry-run
run context mirror dry-run
emit one compact run summary
```

Allowed outputs:

- Ignored generated report under `artifacts/`.
- Console JSON summary.

Forbidden:

- DB writes.
- Evidence writes.
- Case-link writes.
- Source-config mutation.
- OSIR open/bypass.
- Apply/import.
- Commander-ready promotion.
- Launchd install/load/start.
- Browser-private-state access.
- Secrets or `.env` access.

Stop conditions:

- Prefect needs credentials, cloud account state, or secret storage.
- The spike tries to replace launchd before the current loop is further proven.
- The spike cannot remain read-only.
- The spike obscures the existing receipts/status proof chain.

## Multi-Case Live Board Workstream

The one-case board gap is being addressed by a bounded multi-case feature:
the local trigger prompt requests up to five strict current packets, valid
packet subsets from mixed captures can be promoted while invalid packet subsets
are quarantined, and `/external-scout/threads` keeps recent non-updated topics
visible as stale tracked threads before archival.

Completion still requires proof, not just code: a short trigger -> dry-run
capture -> real capture loop must show strict valid multi-packet or explained
fewer-topic output, and a natural cycle must then keep the board current
without invalid packets updating thread state.

## Monitoring Path

V0, already present:

- Prompt-trigger receipts.
- Capture receipts/logs.
- Capture CLI status.
- Thread report dry-run.
- Live Case Board freshness.
- Workstream report.
- Context mirror status.

V1, next:

- Native 24/7 proof report over the latest prompt/capture receipts, health,
  Live Board state, and eval runtime hard-fails:

```bash
.venv/bin/python scripts/report_external_scout_24_7_proof.py --dry-run
```

- Browser/API views: `/external-scout/24-7` and
  `/api/v1/external-scout/24-7-proof`.
- Three consecutive natural `:50 -> :08` cycles are required before calling
  the local Packet-chat production path 24/7-proven.
- AUTOSINT run observability remains on the same `/external-scout/24-7`
  route over local receipts/status artifacts.
- Clear last-success, last-failure, freshness, and skipped/quarantined counts.
- No external tracing.

V2, later:

- Prefect UI for local flow run history, if the spike proves useful.

V3, after agents:

- LangSmith or Phoenix/Arize for sanitized agent/retrieval/eval telemetry.

## Reference Basis

This roadmap is based on current official documentation categories:

- Prefect: Python workflow orchestration, schedules, state tracking, retries,
  and monitoring. Reference: https://docs.prefect.io/v3/get-started
- Airflow: batch-oriented workflow scheduling and monitoring.
  Reference: https://airflow.apache.org/docs/apache-airflow/stable/index.html
- Dagster: asset/data orchestration and lineage orientation.
  Reference: https://docs.dagster.io/
- LangGraph: long-running, stateful agent orchestration with persistence and
  human-in-the-loop support. Reference:
  https://docs.langchain.com/oss/python/langgraph/overview
- LlamaIndex: RAG/indexing/retrieval framework. Reference:
  https://developers.llamaindex.ai/python/framework/
- n8n: workflow automation and integrations. Reference: https://docs.n8n.io/
- LangSmith and Phoenix/Arize: observability/evaluation layers for LLM and agent
  systems. References: https://docs.langchain.com/langsmith/observability and
  https://arize.com/docs/phoenix

## Safety Boundary

This roadmap is advisory and read-only. It does not authorize any migration,
new scheduler ownership, DB mutation, Evidence mutation, case-link mutation,
source-config mutation, OSIR bypass, apply/import path, commander-ready
promotion, credential handling change, or browser-private-state access.
