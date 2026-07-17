# AUTOSINT Theater Watch Policy

The Theater Watch Policy prevents External Scout from becoming an arbitrary
global top-case feed. Case counts are read from the versioned
`config/autosint_system_contract.yml`: the current natural default is 1-3 and
the configured absolute maximum is 5. Every major theater must still be
explicitly accounted for through `theater_watch_summary`.

This is a read-only policy. It does not create Evidence, case links, source-config changes, OSIR exports, apply/import paths, launchd changes, or commander-ready outputs.

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
- `coverage_gaps`
- `deep_dive_recommended`
- `next_check`

`Checked and found` and `Checked and not found` require `checked=true` and a
nonempty source-family itinerary. `Not checked`, `Stale`, and
`Blocked / login required` require `checked=false`, an explicit coverage gap,
and a next check. A missing, duplicate, or unknown theater row is a structural
failure. Seven rows present does not mean seven theaters checked.

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

Only a naturally eligible, validator-clean, preservation-clean, promoted
`GLOBAL_THEATER_SWEEP` with complete coverage advances ignored rotation state.
Failed, quarantined, recovery-assisted, manual, or incomplete cycles do not.
Priority selection never replaces the mandatory due theater. Each theater is
due once within seven successful global cycles.

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
