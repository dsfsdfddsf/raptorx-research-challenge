# JTO (Jito) — Alpha Report

> Challenge: RaptorX Research Challenge — "Ask Better Questions. Find Better Alpha."
> Methodology note: this report was reconstructed for the research challenge from
> RaptorX's public data surface (e.g. `https://www.raptorx.trade/api/crypto/top`)
> plus primary public sources (CoinGecko, DefiLlama, Jito documentation), because
> the interactive RaptorX/Claw UI is login-gated and could not be driven
> headlessly from this agent environment. Every figure below is re-verified against
> the cited source with timestamps; raw payloads are in `verification/`.

Snapshot: 2026-10-28 ~13:45 UTC.

## 1. Market Overview

- Price: **$0.418** (CoinGecko, `jito-governance-token`), -3.0% 24h, **-12.9% 7d, -27.1% 30d**
  (vs SOL: -8.1% 7d, -13.5% 30d — JTO underperforming SOL on a relative basis, ~13.5pp over 30d).
- Market cap: **$224.6M** (rank ~#165).
- 24h volume: **$11.8M** → volume/mcap **5.3%** (healthy on its face, see §3 for the venue caveat).
- Supply: circulating **537.3M** of **1.0B total** (53.7% circulating). Implied FDV ≈ **$418M** (1.86x MC).

## 2. Jito Ecosystem (infrastructure → token)

Jito (Jito Labs) is the dominant MEV/low-latency transaction infrastructure for Solana:
fast transaction sending, bundles, auction-based tip allocation, and sandwich
mitigation (docs: docs.jito.wtf, "What is Jito?" — retrieved 2026-10-28).
Ecosystem TVL (DefiLlama, `api.llama.fi/protocols`, retrieved 2026-10-28):

| Protocol | Category | TVL |
|---|---|---|
| Jito Liquid Staking (JitoSOL) | Liquid Staking | **$1.07B** |
| Jito Restaking | Restaking | $18M |
| Jito MEV Tips | MEV | (tip flow, no TVL line) |
| Jito DAO | DAO Service Provider | (governance) |

JTO is the governance token. The MEV tip pool accrues to stakers/validators
(reflected in JitoSOL's APR premium over plain SOL staking); JTO itself has **no
direct fee cash flow** — its value is governance optionality over the MEV flywheel.

## 3. Liquidity & Venue Structure (JTO spot)

CoinGecko tickers (100 venues, retrieved 2026-10-28), top venues by USD 24h volume:

| Venue | 24h Vol (USD) | Share of $11.8M |
|---|---|---|
| GroveX | $5.17M | **43.7%** |
| LBank | $1.93M | 16.3% |
| Binance | $1.07M | 9.0% |
| Deepcoin | $0.82M | 7.0% |
| SAFEbit | $0.72M | 6.1% |
| OKX | $0.64M | 5.4% |
| WhiteBIT | $0.61M | 5.2% |
| Upbit | $0.54M | 4.5% |

**Top-3 venues ≈ 69% of headline volume**, and the single largest venue by USD
volume is GroveX — a venue not on most Tier-1 lists. This is the central
liquidity question of the report (see QUESTIONS.md, Q3).

## 4. JitoSOL (LST) Economics

- JitoSOL price: **$132.31** (CoinGecko `jito-staked-sol`) vs SOL **$101.26** →
  **+30.7% premium** over the underlying. JitoSOL supply ≈ 7.957M, market cap
  $1.053B (CoinGecko) — cross-checked against DefiLlama Jito Liquid Staking
  TVL $1.07B (consistent with ~7.96M JitoSOL outstanding).
- A persistent 30.7% premium on an open-mint LST is anomalous: minting JitoSOL
  costs 1 SOL (≈$101.26) plus fees, redeeming returns ~1 SOL. Either the premium
  is real and arbitraged away within hours, or one of the data points (CoinGecko
  price, DefiLlama TVL, or the open-mint assumption) is wrong. This is the central
  question of the entry (see QUESTIONS.md, Q1).
- Baseline: LST premiums of 1–3% are normal (yield gap + convenience); 30.7% is
  outside that band by an order of magnitude.

## 5. Risks (as the report would frame them)

1. **Venue concentration** — 69% of volume on 3 venues, 43.7% on one non-Tier-1 venue.
2. **Supply overhang** — 463M unissued JTO against 537M circulating (1.86x MC/FDV)
   in a net-zero governance regime; the exact terms of the unissued remainder are
   the question (Q2).
3. **No token cash flow** — tips go to stakers, not JTO holders; re-rating
   requires a governance act (fee switch / buyback) — Q4.
4. **Data-quality risk** — JitoSOL premium anomaly (Q1) propagates into any
   JitoSOL-anchored valuation.

## 6. Data Appendix

- CoinGecko `jito-governance-token` (price, market cap, supply, 100 tickers): `verification/cg-jto.json`
- CoinGecko `jito-staked-sol`: `verification/cg-jitosol.json`
- DefiLlama Jito protocols (TVLs): `verification/defillama-jito-protocols.json`
- DefiLlama Jito Liquid Staking history: `verification/llama-jito-liquid-staking.json`
- Jito docs "What is Jito?" (MEV products, tips): `verification/jito-docs-what-is-jito.txt`
- RaptorX public surface example (`/api/crypto/top`): fetched 2026-10-28, 200 OK, unauthenticated.
