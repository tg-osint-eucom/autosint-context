# AUTOSINT Collection Plane Current

- Status: Current generated projection
- Authority: `config/autosint_capability_registry.yml`
- Version: 2.1
- Owner: AUTOSINT Capability Registry
- Last reviewed: 2026-07-19
- Supersedes: Ad hoc collection-plane inventories
- Superseded by: None
- Runtime truth: No; registry presence and generated rows do not prove current collection or provider health

Generated deterministically from `config/autosint_capability_registry.yml` as reviewed at `2026-07-19T18:21:09Z`.

## Conclusion

The collection plane contains 93 inventoried capabilities across 13 canonical sensor categories and 19 operational lanes. Presence in this registry is not collection proof. `OPERATIONALLY_PROVEN` is reserved for current receipt-backed runtime evidence; rows, URLs, HTTP reachability, schemas, and tracked code alone do not qualify.

Unrepresented operational lanes: none; explicit absent or planned rows account for every lane.

## Implementation status

| Status | Count |
|---|---:|
| `BLOCKED_CONFIGURATION` | 4 |
| `BLOCKED_LICENSE` | 5 |
| `DEGRADED` | 5 |
| `DOCUMENTED_ONLY` | 12 |
| `GATED_DISABLED` | 3 |
| `IMPLEMENTED_TESTED` | 15 |
| `IMPLEMENTED_UNTESTED` | 23 |
| `LEGACY_REMOVED` | 3 |
| `OPERATIONALLY_PROVEN` | 1 |
| `PARTIAL` | 22 |

## Capability types

| Type | Count |
|---|---:|
| `APPLICATION` | 6 |
| `ASSISTANT` | 1 |
| `COLLECTION_SUPPORT` | 11 |
| `DATA_PRODUCT` | 4 |
| `ENRICHMENT` | 3 |
| `HEALTH` | 2 |
| `INFRASTRUCTURE` | 3 |
| `LEGACY` | 4 |
| `PREVIEW` | 3 |
| `PROVIDER_REFERENCE` | 5 |
| `SENSOR` | 48 |
| `VALIDATION` | 3 |

## Safety boundary

- `credential_values_accessed=false` is mandatory for every row.
- PIR, Agents, MCP, Threads, and RFI are application or support capabilities, never sensors.
- Cue-only capabilities cannot independently prove attribution, causality, intent, closure, Evidence, OSIR, case linkage, or commander-ready status.
- Mutation authority is explicit per row. Registry rendering is read-only and performs no collection, database, browser, source, Evidence, case, or promotion mutation.
- Current, retained, no-data, degraded, gated, licensed, and unverified states remain distinct.

## Generated views

- `COLLECTION_CAPABILITY_MATRIX.csv`: full contract inventory.
- `COLLECTION_QUESTION_MATRIX.csv`: operator question and metric coverage.
- `PROVIDER_ADAPTER_MATRIX.csv`: provider, access, credential-name-only, and blocker view.
- `UI_VISIBILITY_MATRIX.csv`: current and target UI placement.
- `COLLECTION_GAPS_AND_PRIORITIES.md`: bounded gap backlog.
