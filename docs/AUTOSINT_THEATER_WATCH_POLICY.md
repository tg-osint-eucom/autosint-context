# AUTOSINT Theater Watch Policy

The Theater Watch Policy prevents External Scout from becoming an arbitrary
global top-case feed. Case counts are read from the versioned
`config/autosint_system_contract.yml`: the current natural default is 1-3 and
the configured absolute maximum is 5. Every major theater must still be
explicitly accounted for through `theater_watch_summary`.

The current typed evidence identity is `autosint-system-contract-v2.1` with
`autosint-theater-closure-v2.1`. It adds top-level cycle-scoped
`theater_source_checks`, separate from primary-case `source_checks`.

This is a read-only policy. It does not create Evidence, case links, source-config changes, OSIR exports, apply/import paths, launchd changes, or commander-ready outputs.

Configured bounded sweep only.
This does not assert exhaustive coverage of all world events.

## Required Theater Summary

Every normal natural cycle uses `cycle_scope=GLOBAL_THEATER_SWEEP` and includes
exactly one top-level `theater_watch_summary` row for each workspace:

- `SOCCENT`
- `SOCEUR`
- `SOCPAC`
- `SOCAFRICA`
- `SOCSOUTH`
- `SOCKOR`
- `SOCOMD`

Every row includes:

- `theater`
- `checked`
- `sweep_status`
- `window_start`
- `window_end`
- `active_case_found`
- `emitted_packet_id`
- `top_candidate_topic`
- `top_watched_topics`
- `candidate_count`
- `source_families_checked`
- `family_results`
- `coverage_gaps`
- `deep_dive_recommended`
- `next_check`

`Checked and found` and `Checked and not found` require `checked=true` and
evidence-backed completion of every configured minimum source family.
`Not checked`, `Stale`, and `Blocked / login required` require `checked=false`,
an explicit coverage gap, and a next check. A missing, duplicate, or unknown
theater row is a structural failure. Seven rows present does not mean seven
theaters checked.

The same-source proof object reports these dimensions separately:

- `theaters_required`: the configured seven-theater set;
- `theaters_swept`: rows actually checked in the current bounded window;
- `theaters_verified_complete`: swept, current rows whose configured minimum
  source families are all evidence-backed complete with zero theater semantic
  and closure validation errors;
- `theaters_candidate_only`: swept rows with candidates that were not
  imported;
- `theaters_not_checked`, `theaters_stale`, and `theaters_blocked`: explicit
  incomplete states.

## Evidence-Backed Minimum-Family Closure

Every theater requires exactly one current `family_results` result for each
configured minimum family:

- `Official / Advisory`
- `Public News`
- `Multilingual / Regional`

Every top-level `theater_source_checks` row contains:

- `source_check_id`, `theater`, and `source_family`
- `primary_status` and exact `check_method`
- `checked_at`, `window_start`, `window_end`, and `current_window`
- exact `public_access_mode`
- exact `completion_basis`
- `source_urls`, `result_summary`, `limitations`, and `next_check`

Source-check `result_summary` and optional `check_method_note` are informational
only and never affect completion. Optional
`adapter_result_ref` is usable for completion only after trusted AUTOSINT
runtime resolution.

Machine-owned `source_check_completion_basis_by_primary_status` defines the
exact status pairing. Completion bases are:

- `substantive_content`: pairs only with `Checked and found`
- `bounded_no_result`: pairs only with `Checked and not found`
- `none`: pairs only with `Candidate found, not imported`, `Not checked`,
  `Stale`, or `Blocked / login required`

Any other basis/status pairing is a hard validation error and is never
downgraded. Opaque `source_check_id` and `evidence_refs` values must match
`^[A-Za-z0-9][A-Za-z0-9:_-]{0,95}$`. URLs, JWTs, signed strings, and values
containing `/`, `.`, `?`, `=`, or `@` are invalid IDs.

Exact method codes are:

- `bounded_official_advisory_review`
- `bounded_public_news_review`
- `bounded_multilingual_regional_review`
- `approved_read_only_adapter`
- `not_checked`

Family/method ownership is exact:

- `Official / Advisory`: `bounded_official_advisory_review` or
  `approved_read_only_adapter`
- `Public News`: `bounded_public_news_review` or
  `approved_read_only_adapter`
- `Multilingual / Regional`: `bounded_multilingual_regional_review` or
  `approved_read_only_adapter`

Exact public-access modes are:

- `public_no_login`
- `approved_read_only_adapter`
- `blocked_login_or_license`
- `candidate_only`
- `not_checked`

The bounded method must match its source family. Generic prose in
`check_method` is invalid and never proves a check. An
`approved_read_only_adapter` row remains `GATED_DISABLED` unless its
`adapter_result_ref` resolves to a trusted current runtime record.

Each assistant family result contains `source_family`,
`reported_primary_status`, `reported_coverage_status`, `evidence_refs`,
`checked_not_found`, `follow_up_statuses`, `result_summary`, `limitations`, and
`next_check`. Every `evidence_refs` value must identify a unique source-check
row from the same output, theater, and source family. Only evidence references
credited to `Checked and found` or `Checked and not found` completion must be
current-window. Stale and candidate follow-up references are allowed, remain
incomplete, and never receive completion credit.

A family is complete only when either:

- `reported_primary_status=Checked and found` references
  `completion_basis=substantive_content` current evidence with an allowed
  method and access, plus a safe public source URL or trusted adapter result
  reference; or
- `reported_primary_status=Checked and not found` references
  `completion_basis=bounded_no_result` current evidence with an allowed method
  and access, plus a safe public itinerary URL or trusted adapter result
  reference and zero validated found sources. Its family result must set
  `checked_not_found=true` and state that no credible current result was found;
  that phrase is a hard consistency requirement but is never completion proof.

`Candidate found, not imported`, `Not checked`, `Stale`, and
`Blocked / login required` are honest incomplete primary states. Candidate,
blocked, and stale sources remain visible follow-ups and never count as
coverage proof. Candidate URLs, HTTP availability, titles, snippets, and
generic prose also never prove coverage. A follow-up never downgrades an
already complete primary family result. If a real bounded itinerary finds no
credible current event, use `Checked and not found`; never fabricate a case to
obtain 7/7.

AUTOSINT derives `canonical_primary_status`, `canonical_coverage_status`,
`checked_source_count`, `validated_source_count`, `candidate_source_count`,
`blocked_source_count`, `stale_source_count`, currentness, and
`theater_verified_complete`. Assistant-reported status or counts are never
authoritative.

The same-source proof object derives one closure-evidence row per theater with
the sweep window, required and completed minimum families, canonical family
results, verified/not-found/follow-up counts, current coverage status,
`theater_verified_complete`, limitations, next check, cycle timestamp,
`source_cycle_id_hash`, and `mutation_performed=false`.

`theater_source_check_validation_error_count`,
`theater_closure_validation_error_count`, and
`candidate_as_coverage_error_count` are V2.1 promotion gates. A valid present
but incomplete family increments `minimum_family_gap_count`; that diagnostic
alone does not block promotion, so an honest incomplete packet may refresh
current state. Coverage remains incomplete and rotation receives no credit.
Historical `autosint-system-contract-v2` /
`autosint-theater-closure-v1` rows remain legacy replay context with closure
status `UNKNOWN` and
`theater_verified_complete=false`; they are never silently reinterpreted as
typed V2.1 evidence.

Explicit bounded recovery uses `cycle_scope=FOCUSED_THEATER_DEEP_DIVE`, exactly
one honest theater row, `recovery_assisted=true`, and
`natural_cycle_eligible=false`. It does not claim global coverage and does not
advance rotation.

When credible cases exceed the configured absolute maximum, emitted cases stay
within that maximum and the rest go into `overflow_candidate_cases` with a
clear reason.

## Deep-Dive Rotation

Tracked code selects one oldest-due mandatory theater for each successful
global cycle. A distinct current-priority theater may occupy the second slot;
one severe or fast-changing theater may occupy the optional third slot.

Only a naturally eligible, validator-clean, preservation-clean, closure-clean,
promoted `GLOBAL_THEATER_SWEEP` with evidence-backed complete coverage advances
ignored rotation state. Failed, quarantined, recovery-assisted, manual, or
incomplete cycles do not.
Priority selection never replaces the mandatory due theater. Each theater is
due once within seven successful global cycles.

Every reported deep-dive slot exposes `deep_dive_performed`,
`rotation_credit_eligible`, `rotation_credit_awarded`, and
`rotation_credit_reason`. Only the mandatory oldest-due slot can receive
rotation credit. The stable reason vocabulary is:

- `credited_complete_natural_cycle`
- `global_coverage_incomplete`
- `recovery_assisted`
- `cycle_ineligible`
- `validation_failed`
- `promotion_failed`
- `duplicate_event`
- `missing_deep_dive_evidence`

These fields explain the existing strict policy; they do not relax or alter
rotation eligibility. A performed deep dive is not automatically a credited
deep dive.

## Cross-Theater Identity

Every emitted case carries `global_event_key`, `primary_theater`,
`supporting_theaters`, `duplicate_of`, and `cross_theater_reason`. One
real-world event has one primary case/thread; supporting theaters retain a
reference to that same thread.

Korea Peninsula events use `SOCKOR` as primary and may add `SOCPAC` as
supporting context. `SOCOMD` is the `cross_theater_strategic_rollup`; regional
events keep their regional primary and may add `SOCOMD` as supporting command
context. `SOCOMD` is primary only for a genuinely global, command-wide, or
cross-theater event.

## Separate Truth Dimensions

- Runtime proof remains the canonical three-consecutive-natural-cycle
  reliability proof.
- `global_theater_coverage_status` reports `COMPLETE`, `INCOMPLETE`, `STALE`,
  or `UNKNOWN` for the current collection window.
- `deep_dive_rotation_status` reports `CURRENT`, `DUE`, `OVERDUE`, or
  `UNINITIALIZED`.

`PROVEN` does not imply seven theaters were checked. One explicit `Not checked`
row makes coverage WARN/incomplete but does not by itself reset runtime proof.
One receipt-backed naturally scheduled V2.1 cycle may establish typed-contract
natural acceptance; it does not establish the separate three-consecutive-cycle
`PROVEN` reliability gate. This policy does not claim that either state is
current.

## Starter Theater Policies

### SOCCENT

Priority topics: Hormuz/Gulf maritime risk, Lebanon/Israel/Hezbollah, Syria/Iraq/ISIS, Red Sea/Yemen, Gulf energy/logistics.

Languages: Arabic, Farsi/Persian, Hebrew, Turkish, Kurdish, English.

Core sensors: official maritime advisories, CENTCOM/public command releases, Reuters/AP/AFP/BBC/regional/trade press, AIS, IMF PortWatch, NASA FIRMS, Sentinel/Copernicus, weather/sea state, oil/energy, shipping/tanker, defense and regional markets, Polymarket/Kalshi, public OSINT communities.

### SOCEUR

Priority topics: Ukraine energy/refinery/logistics strikes, Black Sea, Russian infrastructure, NATO/EU security.

Languages: Ukrainian, Russian, English, relevant regional European languages.

Core sensors: official Ukrainian/NATO/EU/national defense releases, public news, energy/logistics trade press, rail/logistics/port reporting, NASA FIRMS, Sentinel/Copernicus, public geospatial reports, weather/smoke/fire context, regional/energy/defense markets, Polymarket/Kalshi, public OSINT.

### SOCPAC

Priority topics: Taiwan/China grey-zone, South China Sea, Korea, Philippines/Japan maritime.

Languages: Mandarin, Japanese, Korean, English, relevant Southeast Asian languages.

Core sensors: Taiwan/Japan/Philippines/South Korea/USINDOPACOM public releases, Reuters/AP/AFP/BBC/regional media, AIS, OpenSky/ADS-B, public port/vessel reporting, Sentinel/Copernicus, public geospatial reports, weather/sea state, regional/defense/shipping markets, Polymarket/Kalshi, public OSINT.

### SOCAFRICA

Priority topics: Sahel security, Sudan/Red Sea spillover, Somalia/Horn of Africa, strategic airports and ports.

Languages: Arabic, French, English, relevant local languages where public sources are available.

Core sensors: UN/AU/AFRICOM/national releases, Reuters/AP/AFP/BBC/regional media, humanitarian/logistics reporting, airport/port public notices, OpenSky/ADS-B when relevant, NASA FIRMS, Sentinel/Copernicus, weather/environment context, regional/oil/crypto market cues, public OSINT.

### SOCSOUTH

Priority topics: Caribbean and Latin America maritime/security incidents, migration/logistics disruption, critical infrastructure or energy disruption.

Languages: Spanish, Portuguese, English, French where relevant.

Core sensors: national official releases, SOUTHCOM, coast guard/maritime advisories, public news, regional media, AIS, port/terminal notices, OpenSky/ADS-B, NASA FIRMS, Sentinel/Copernicus, tropical/weather hazards, regional/oil/shipping/crypto market cues, public OSINT.

### SOCKOR

Priority topics: North Korea missile/nuclear indicators, Korea Peninsula maritime/air incidents, South Korea infrastructure/security incidents.

Languages: Korean, English, Japanese, Mandarin when relevant.

Core sensors: South Korea JCS/MND, Japan MOD, USFK/INDOPACOM, UN where relevant, Reuters/AP/AFP/BBC/regional media, OpenSky/ADS-B, maritime public reporting, public infrastructure notices, Sentinel/Copernicus, public imagery, regional/defense/crypto market cues, public OSINT.

### SOCOMD

Priority topics: global SOCOM-wide emerging risk, cross-theater source gaps, strategic logistics or command-relevant incidents.

Languages: English plus theater-specific languages inherited from the affected region.

Core sensors: SOCOM/public command releases, relevant theater official sources, public news/trade sources, theater-specific movement/geospatial/weather sources, broad/defense/crypto market cues, Polymarket/Kalshi, public OSINT.

## Live Board Semantics

The Live Case Board should show:

- active threads from latest valid packets,
- stale tracked threads from the rolling 72-hour window,
- archived historical threads beyond the window,
- theater rows even when no packet was emitted,
- overflow candidate cases,
- source/sensor coverage status.

Invalid or quarantined packets never update current threads. Lower-quality packets do not replace best current state.
