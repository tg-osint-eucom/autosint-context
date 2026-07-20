# AUTOSINT MCP Boundary V1

- Status: Current tracked MCP contract
- Authority: `scripts/autosint_mcp_server.py` and the generated root inventories
- Version: 1.0
- Owner: AUTOSINT MCP
- Runtime truth: No; external Codex rebind, reload, and live handshake require a separate current receipt
- Last reviewed: 2026-07-19
- Supersedes: Legacy-checkout MCP binding and single-flag write authorization
- Superseded by: None
- Canonical repository class: `autosint-clean-20260621`

## Conclusion

The AUTOSINT MCP server is canonical-repository-only and read-only by default.
Its current registered surface contains 33 tools, 12 resources, and 1 prompt:

- 26 tools are `READ_ONLY`;
- 7 tools are exceptional mutation surfaces;
- every resource is `READ_ONLY`;
- the only prompt is restricted to five named read tools;
- every write gate is OFF when its environment variable is absent;
- the legacy `AUTOSINT_MCP_ALLOW_AGENT_WRITES` variable is not authorization.

This tracked contract does not prove that Codex is rebound to this server. It
does not start or reload MCP. The external configuration rebind and read-only
handshake must be performed separately and recorded as current runtime
evidence.

## Machine-Owned Inventories

The deterministic checker derives inventories from the live FastMCP
registrations and the server-owned contract map:

- `MCP_TOOL_INVENTORY.csv`
- `MCP_RESOURCE_INVENTORY.csv`
- `MCP_PROMPT_INVENTORY.csv`
- `MCP_MUTATION_AUTHORITY_MATRIX.csv`

Run the no-write drift check with:

```bash
PYTHONPATH=src:. .venv/bin/python scripts/check_autosint_mcp_inventories.py --check
```

`--write` is a deliberate tracked-file maintenance action. It is not used by
the MCP server and is never an MCP write path.

## Canonical Repository Guard

`canonical_repo_required=true` applies to every tool, resource, and prompt.
The server verifies all of the following without publishing a private absolute
path in the tracked contract:

1. repository leaf name is exactly `autosint-clean-20260621`;
2. `git rev-parse --show-toplevel` resolves to the loaded project root;
3. `AGENTS.md` exists at that root;
4. `scripts/autosint_mcp_server.py` exists at that root.

Startup fails closed with `WRONG_REPO` when any check fails. Tool, resource,
and prompt dispatch also checks the repository class, so an in-process caller
cannot bypass the startup check. `system_status` exposes the bounded
`mcp_boundary.canonical_repo` classification and boolean checks for a safe
handshake.

## Mutation Classes

| Class | Registered tools | Default |
| --- | --- | --- |
| `READ_ONLY` | 26 inventory-listed tools | Available in the canonical repo |
| `ARTIFACT_WRITE` | None | Gate OFF |
| `DB_WRITE` | None | Gate OFF |
| `EVIDENCE_WRITE` | None | Gate OFF |
| `CASE_LINK_WRITE` | None | Gate OFF |
| `SOURCE_CONFIG_WRITE` | None | Gate OFF |
| `OSIR_WRITE` | `export_osir_package` | Gate OFF |
| `AGENT_EXCHANGE_WRITE` | `create_case`, `post_finding_card`, `post_agent_packet`, `vote_on_finding`, `flag_source_conflict` | Gate OFF |
| `CONTROL_ACTION` | `run_daily_cycle` | Gate OFF |

`post_finding_card` is classified by its owning Agent Exchange API boundary.
Its inventory also discloses that it may create bounded case overlay links.
It never mutates raw Evidence. There is no registered general
`CASE_LINK_WRITE` tool.

## Fail-Closed Write Authorization

Every non-read tool evaluates the same ordered policy:

1. canonical repository class must pass;
2. global `AUTOSINT_MCP_ALLOW_ACTIONS=1` must be present in the server process;
3. the exact class gate must equal `1`;
4. the call must include `allow=true`;
5. the call must include a bounded safe `scope` identifier;
6. `scope` must exactly match the machine-derived target scope;
7. the tool-specific deterministic policy remains authoritative;
8. the response must contain `audit_receipt` and `mutation_performed`.

No one condition substitutes for another. In particular, a class gate without
the global gate, a global gate without the class gate, a legacy gate, an
implicit target, or a plausible scope is denied.

Exact class gates are:

| Class | Environment gate |
| --- | --- |
| `ARTIFACT_WRITE` | `AUTOSINT_MCP_ALLOW_ARTIFACT_WRITE` |
| `DB_WRITE` | `AUTOSINT_MCP_ALLOW_DB_WRITE` |
| `EVIDENCE_WRITE` | `AUTOSINT_MCP_ALLOW_EVIDENCE_WRITE` |
| `CASE_LINK_WRITE` | `AUTOSINT_MCP_ALLOW_CASE_LINK_WRITE` |
| `SOURCE_CONFIG_WRITE` | `AUTOSINT_MCP_ALLOW_SOURCE_CONFIG_WRITE` |
| `OSIR_WRITE` | `AUTOSINT_MCP_ALLOW_OSIR_WRITE` |
| `AGENT_EXCHANGE_WRITE` | `AUTOSINT_MCP_ALLOW_AGENT_EXCHANGE_WRITE` |
| `CONTROL_ACTION` | `AUTOSINT_MCP_ALLOW_CONTROL_ACTION` |

The server configuration should omit all of them. Enabling a gate is an
explicit per-process operational decision and still does not authorize a call
without `allow=true` and exact scope.

## Exact Scopes

| Tool | Required scope |
| --- | --- |
| `create_case` | `case:new` |
| `export_osir_package` | `case:<canonical UUID>` |
| `post_finding_card` | `case:<canonical UUID>` |
| `post_agent_packet` | `case:<canonical UUID>` |
| `vote_on_finding` | `finding-card:<canonical UUID>` |
| `flag_source_conflict` | `finding-card:<canonical UUID>` |
| `run_daily_cycle` | `cycle:daily` |

UUID targets are normalized before they are included in a receipt. Invalid or
unbounded identifiers are represented as an invalid target classification;
raw arbitrary input is not copied into receipt scope fields.

## Deterministic Policy And Audit Receipt

Each mutation tool has one server-selected `policy_id`. The caller cannot
select or weaken it. `policy_sha256` is deterministically calculated from:

- boundary version;
- tool name;
- mutation class;
- global and exact class gates;
- per-call confirmation requirement;
- scope rule;
- policy identifier;
- receipt schema.

Every allowed or denied mutation call returns an
`autosint-mcp-audit-receipt-v1` object with:

- `receipt_id`;
- `evaluated_at`;
- `tool_name` and `mutation_class`;
- `policy_id` and `policy_sha256`;
- `repo_class` and `canonical_repo_required`;
- global/class gate booleans;
- per-call `allow` and bounded `scope`;
- expected scope;
- decision and authorization state;
- outcome status;
- `mutation_performed`.

The receipt is returned in the tool result. A denied request does not write a
receipt artifact because doing so would turn a denial into a separate artifact
mutation and create a competing audit store.

## `mutation_performed` Semantics

- Repository, gate, confirmation, scope, validation, and internal-policy
  denials return `false`.
- Agent Exchange tools return `true` only after the bounded transaction
  commits.
- `export_osir_package` returns `false` when the pre-write OSIR policy gate
  denies export and `true` after the artifact writer is dispatched. A
  post-dispatch error is conservatively reported as `true` because a partial
  filesystem effect cannot be disproved.
- `run_daily_cycle` returns `false` for pre-dispatch blockers and `true` once
  the existing runner is dispatched, even when its return code is nonzero.

This field reports mutation effect/dispatch truth; it does not certify that the
requested business outcome succeeded.

## Hardened Exceptional Tools

### `export_osir_package`

The tool now requires the global and `OSIR_WRITE` gates, `allow=true`, and the
exact case scope. It performs a read-only canonical OSIR eligibility check
before calling the artifact writer. The existing OSIR policy remains an
independent, mandatory inner gate. Nothing in MCP bypasses Evidence quality,
QA, case status, or OSIR eligibility rules.

### Agent Exchange writes

All five write tools share the global and `AGENT_EXCHANGE_WRITE` gates plus
tool-specific policy and exact scope. Successful DB commit is the only success
path that returns `mutation_performed=true`. These tools do not grant raw
Evidence, source-config, commander-ready, or autonomous routing authority.

### `run_daily_cycle`

The tool requires the global and `CONTROL_ACTION` gates, `allow=true`, and
`scope=cycle:daily`. Port and runner checks occur before dispatch. This tool is
not a natural-cycle proof source; invocation through MCP is an explicitly
assisted control action and must not be credited as a natural External Scout
cycle.

## Safe Read Compatibility

Existing read tool names, parameters, resources, and prompt name remain
registered. FastMCP tool annotations and metadata expose:

- `readOnlyHint`;
- `canonical_repo_required`;
- `read_only`;
- mutation class;
- gates and policy for exceptional tools.

The `analyst_brief` prompt names only:

- `system_status`;
- `database_pulse`;
- `recent_events`;
- `event_detail`;
- `read_executive_summary`.

It explicitly prohibits exports, Agent Exchange writes, collection actions,
and all other non-read tools.

## Safety Boundary

This MCP contract does not authorize or perform:

- raw Evidence writes;
- source registry/config changes;
- general case-link writes;
- OSIR bypass or commander-ready promotion;
- private browser/session-state access;
- credential or `.env` value disclosure;
- External Scout prompt/harvester recovery;
- launchd mutation;
- MCP rebind, reload, or live server launch.

The Codex configuration must be handled as a separate bounded external step.
Only the `[mcp_servers.autosint]` block may be changed, and the resulting
read-only handshake must prove the canonical repo class and all write gates
OFF.
