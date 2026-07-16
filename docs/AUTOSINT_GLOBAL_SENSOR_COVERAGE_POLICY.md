# AUTOSINT Global Sensor Coverage Policy

This policy defines the source and sensor lanes that every serious External Scout case must account for before it can be treated as preview-safe on the Live Case Board or in RFI.

AUTOSINT still treats every External Scout packet as candidate input only. This policy does not authorize DB writes, raw Evidence writes, case links, source-config mutation, OSIR export, apply/import, commander-ready promotion, credentialed collection, login bypass, CAPTCHA bypass, or private browser-state access.

## Core Rule

No required source or sensor lane may be silently omitted.

Every lane must report one of these statuses:

- `Checked and found`
- `Checked and not found`
- `Candidate found, not imported`
- `Not checked`
- `Stale`
- `Blocked / login required`

Explicit `Not checked`, `Stale`, or `Blocked / login required` is honest lane
accounting only. It does not prove that collection was performed, that the lane
is complete, or that a provider adapter is healthy.

If a lane is cue-only, the packet must say so. Markets, crypto, prediction markets, social OSINT, and public comments cannot independently prove closure, reopening, attribution, causality, intent, insider activity, or commander-ready status.

## Required Lanes

| Lane | Required coverage | Cue-only |
|---|---|---|
| Official / Advisory | Government/official statements, maritime/aviation advisories, public command releases, UN/NATO/EU or relevant multinational bodies. | No |
| Public News | Reuters, AP, AFP/BBC, regional media, relevant trade press. | No |
| Social OSINT | Public X/Twitter, OSINT613, OSINTdefender/sentdefender, public Telegram mirrors, Reddit/public forums, local public communities. | Yes |
| Traffic / Movement | AIS, IMF PortWatch, GFW when relevant, OpenSky/ADS-B when aviation-relevant, public port/terminal/vessel/flight movement reporting. | No |
| Satellite / Geospatial | NASA FIRMS, Sentinel/Copernicus, public SAR/optical reporting, public geospatial reports. | No |
| Weather / Environment | Weather, sea state, visibility, smoke/fire/dust/haze, environmental context. | Context only |
| Markets / Finance | Broad market, oil/energy, shipping/tanker, defense large-cap, defense mid/small, regional market, crypto/risk, insurance/freight/rates where relevant. | Yes |
| Prediction Markets | Polymarket, Kalshi, Manifold/other public markets when relevant; probability/price, volume/liquidity/open interest if visible, settlement criteria, comments availability. | Yes |
| Multilingual / Regional | Theater-specific languages, regional official/media sources, direct public local-language claims, translation summaries, missing-language caveats. | No |
| Public Comments / Reaction | Public visible comments only. | Yes |

## Required Row Fields

Every lane row should include:

- `status`
- `summary`
- `source_urls`
- `retrieved_at` or timestamp if available
- `what_it_suggests`
- `what_it_does_not_prove`
- `collection_gap`
- `next_check`
- `cue_only`

The current packet validator enforces the strict packet matrices and accepted status vocabulary. The Live Case Board separately distinguishes:

- `Required Coverage Matrix`: whether required schema sections are present and preview-safe.
- `Source Checks`: whether current source-check rows are fully checked.
- `Follow-up Gaps`: whether follow-up collection remains.

Matrix complete does not mean every possible source lane has been exhausted.

## Safety

This policy is read-only. It is not a source registry mutation and does not change collector behavior by itself. Runtime collection must remain public-only unless the user explicitly approves credentialed collection later.
