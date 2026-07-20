# AUTOSINT Trust And Assurance Model

- Status: Proposed
- Authority: Safety and assurance design proposal
- Version: 1.0
- Owner: AUTOSINT Assurance
- Last reviewed: 2026-07-15
- Runtime truth: No; evidence must be checked per run
- Supersedes: None
- Superseded by: None
- Related: [Architecture Audit Question Bank](AUTOSINT_ARCHITECTURE_AUDIT_QUESTION_BANK.md), [Target Data Lifecycle](AUTOSINT_TARGET_DATA_LIFECYCLE.md), [Primary Workflow](AUTOSINT_PRIMARY_WORKFLOW.md)

## Assurance Position

AUTOSINT trust is earned per claim and transformation. It is not inherited from a model name,
provider, route, screenshot, schema pass, or marketing analogy. This proposal is informed by the
voluntary NIST AI RMF functions `Govern`, `Map`, `Measure`, and `Manage`, and by the DoD
Responsible AI Strategy and Implementation Pathway. It does not claim compliance,
certification, accreditation, or DoD adoption.

Official references checked 2026-07-16:

- NIST AI RMF 1.0: <https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10>
- NIST AI RMF Core: <https://airc.nist.gov/airmf-resources/airmf/5-sec-core/>
- DoD Responsible AI initiative: <https://www.ai.mil/Initiatives/Responsible-AI/index.html>
- DoD Responsible AI Strategy and Implementation Pathway: <https://www.ai.mil/Portals/137/Documents/Resources%20Page/DoD%20Responsible%20AI%20Strategy%20and%20Implementation%20Pathway.pdf>

## Framework Mapping

| AUTOSINT proposal area | NIST AI RMF influence | DoD RAI influence | Bounded AUTOSINT interpretation |
|---|---|---|---|
| Governance record and closed authorities | `GOVERN` | Responsible and governable use | Named owner, scope, mutation authority, review date, and explicit closed gates. |
| Input/mission context and source gaps | `MAP` | Traceable and responsible use | Record intended use, source status, missing lanes, cue-only limits, and affected operator surface. |
| Validation, replay, and preservation metrics | `MEASURE` | Reliable and traceable behavior | Test identity, semantic completeness, preservation, uncertainty, and failure modes. |
| Quarantine, degraded states, and recovery | `MANAGE` | Governable and reliable operation | Fail closed, retain provenance, expose blockers, and require bounded review before recovery. |

This mapping is design guidance only. It is not a control assessment or a
statement that every framework outcome has been implemented.

## Trust States

| State | Meaning |
|---|---|
| `UNVERIFIED_INPUT` | Source or model output has not passed canonical checks. |
| `CANDIDATE` | Structured input exists but has no production authority. |
| `VALIDATED_CANDIDATE` | Required deterministic checks passed. |
| `CONTRADICTED` | Material conflicting evidence is present. |
| `QUARANTINED` | Identity, schema, semantic, freshness, or policy gate failed. |
| `RETAINED_STALE` | Last-known-good continuity context, not current truth. |
| `OPERATOR_REVIEWED` | Human reviewed the trace and recorded a decision. |
| `RETRACTED` | Prior claim/relationship is no longer valid but remains auditable. |

None of these automatically means Evidence, OSIR, apply/import, or commander-ready.

## Claim Assurance Card

Every operator-facing claim should expose:

- claim text and state;
- observed facts versus inference;
- source and independent source-family counts;
- source quality and freshness;
- corroborating and contradicting references;
- missing required lanes;
- cue-only inputs;
- model contribution and model/version;
- deterministic checks and results;
- transformation and receipt references;
- what it suggests and does not prove;
- what would change the assessment;
- next safe action;
- human decision and timestamp when present.

## Assurance Gates

### Input Gate

Require source identity, access status, observation/publication timestamps, immutable artifact
reference, lane/category mapping, and cue-only/proof-capable state.

### Transformation Gate

Require input/output hashes, code/contract version, field-preservation result, defaults inserted,
fields dropped or rejected, and receipt.

### Model Gate

Require intended surface, model/version identity when verifiable, prompt contract, bounded inputs,
budget/timeout, output state `CANDIDATE`, and deterministic validation. Desired UI selection is not
runtime attribution without exact evidence.

### Relationship Gate

Require relationship type, temporal validity, source/evidence references, source independence,
contradiction state, confidence basis, proposer, validator/approver, and retraction behavior.

### Promotion Gate

Require exact request identity, freshness/newer-than-current, validation errors `0`, complete
required semantics, no partial-promotion violation, and a receipt. Schema validity alone is not
semantic completeness.

### Operator Gate

Require read-only trace, current/stale state, uncertainty, contradictions, missing data, next safe
action, and bounded acknowledgement. High-impact decisions remain outside candidate projections.

## Independent Verification

At least one of the following must verify a high-impact conclusion:

1. deterministic rule or validator;
2. replay against fixed source artifacts;
3. independent model/agent with isolated evidence and declared correlation risk;
4. human review.

The same model paraphrasing its own output is not independent verification.

## Proof Versus Health

Health describes current operational risk. Proof establishes the required evidence chain.
`WARN_WITH_NO_RED` is not automatically proof. Retained data can support continuity while proof is
invalid. External Scout `PROVEN` remains controlled only by the canonical same-source proof report.

## Governance Record

Every architecture or policy exception records owner, scope, rationale, data tier, mutation
authority, expiry/review date, tests, runtime proof requirement, rollback, and approver. Temporary
operator recovery cannot silently become permanent architecture.

## Assurance Metrics

- source-to-claim trace completeness;
- raw-to-normalized field preservation;
- unsupported-edge rejection rate;
- contradiction detection and resolution time;
- stale/current labeling accuracy;
- validator false accept/false reject rates;
- operator review time and correction rate;
- model fallback success;
- replay reproducibility;
- receipt coverage;
- privacy/secret scan findings.

## Closed Authorities

The normal operator path cannot automatically:

- create Evidence;
- create or mutate case links;
- alter source configuration;
- open OSIR gates or export approval;
- apply/import candidate state;
- mark commander-ready;
- invoke Agent or PIR writes;
- execute Operator Scheduler.
