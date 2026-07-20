# AUTOSINT Capability Registry Current

- Status: Current generated projection
- Authority: `config/autosint_capability_registry.yml`
- Version: 2.1
- Owner: AUTOSINT Capability Registry
- Last reviewed: 2026-07-19
- Supersedes: Ad hoc capability inventories
- Superseded by: None
- Runtime truth: No; inventory and implementation labels do not prove current operational health

## Authority

`config/autosint_capability_registry.yml` is the canonical V2.1 capability inventory. Its schema is `schemas/autosint_capability_registry.schema.json`. This document is generated, not a parallel truth source.

- Registry review timestamp: `2026-07-19T18:21:09Z`
- Capability records: 93
- Canonical sensor categories: 13
- Operational lanes: 19
- Credential values accessed while building the registry: `false`

## Truth rules

- `IMPLEMENTED_TESTED` is code/test evidence only.
- `OPERATIONALLY_PROVEN` additionally requires current receipt-backed runtime evidence in the same row.
- `BLOCKED_CONFIGURATION` names configuration variables only; it never proves a credential value exists.
- `BLOCKED_LICENSE` remains distinct from technical failure.
- `LEGACY_REMOVED` is not an invitation to restore a second application or truth source.
- A sensor-registry row is an inventory record, not proof that the sensor checked the current case.

## Status summary

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

## Type summary

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

## Validation

Run `python scripts/check_autosint_capability_truth.py --registry-only` and `python scripts/render_autosint_capability_registry.py --check`. Both commands are read-only in check mode.
