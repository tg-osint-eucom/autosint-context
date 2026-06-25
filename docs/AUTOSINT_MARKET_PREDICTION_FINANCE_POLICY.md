# AUTOSINT Market Prediction Finance Policy

This policy makes market, prediction-market, finance, defense-equity, shipping, insurance, regional-market, and crypto/risk checks a persistent cue-only enrichment layer for every active External Scout Live Case Board thread.

## Core Rule

No active thread may silently omit a required market/prediction/finance lane. Each lane must be explicitly reported as one of:

- `Checked and found`
- `Checked and not found`
- `Candidate found, not imported`
- `Not checked`
- `Stale`
- `Blocked / login required`

`Checked and not found` is acceptable when the check is explicit. `Blocked / login required` is allowed when a public source blocks access, but it remains a follow-up gap. `Not checked` makes the market/prediction/finance status `Partial`.

## Cue-Only Boundary

Markets, prediction markets, crypto, social posts, and public comments are cue-only. They may support HAVOC/RFI preview context, but they never prove closure, reopening, intent, causality, attribution, insider activity, or commander-ready status. They do not open OSIR, create Evidence, create case links, mutate source config, or perform apply/import.

## Required Lanes

Prediction-market lanes:

- Polymarket
- Kalshi
- Manifold or other relevant public markets

Market/finance lanes:

- Broad market: SPY, QQQ, VIX, DXY, treasuries/rates where public.
- Oil / energy: Brent, WTI, USO, BNO, XLE, natural gas/LNG proxies where relevant.
- Shipping / tanker: FRO, STNG, TNK, DHT, EURN, INSW, Maersk, ZIM, and public tanker/freight/rate sources.
- Insurance / freight / rates: public P&I/insurer notes, war-risk premium reporting, Baltic Dirty/Clean Tanker public sources, and public tanker day-rate reporting.
- Defense large-cap: LMT, RTX, NOC, GD, HII, BA, BAE Systems, Thales, Leonardo, Rheinmetall, Saab, Elbit, and equivalents.
- Defense mid/small: AVAV, KTOS, TXT, QinetiQ, and public drone/UAS/naval/sensor suppliers.
- Regional markets by theater: Gulf/Saudi/Qatar/UAE/Oman for SOCCENT, Europe/Ukraine/Russia-exposed proxies for SOCEUR, Taiwan/China/Japan/Korea/Philippines for SOCPAC, and relevant regional proxies for the remaining SOC workspaces.
- Crypto / risk: BTC, ETH, and public stablecoin/risk-flow cues where relevant.

`Insurance / freight / rates` must be present as the explicit
`market_finance_matrix.insurance_freight_rates` lane. The broader
`Shipping / Logistics / Insurance` case-coverage category is not sufficient by
itself.

## Required Row Content

Every lane should record:

- status
- instruments checked
- values/change/timestamp if available
- public URL or source/tool note
- interpretation
- what it does not prove
- next check
- cue-only flag

## Operator Display

The Live Case Board and HAVOC/RFI surfaces distinguish:

- `Required Coverage Matrix`: required schema sections are present and preview-safe.
- `Source Checks`: broader source lanes are fully checked or still partial.
- `Market/Prediction/Finance Check Status`: strict market/prediction/finance lane completeness.
- `Follow-up Gaps`: remaining source or lane checks that need attention.

`Ready for HAVOC/RFI Preview` can coexist with `Market/Prediction/Finance Check Status: Partial`; preview readiness is not commander-ready status.
