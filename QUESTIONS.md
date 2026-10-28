# REX AI 5.0 — "Ask Better Questions" (JTO report)

Each question below is written verbatim as a prompt to REX AI 5.0 (the follow-up
chat of the JTO report in REPORT-JTO.md). Each starts from a specific line of the
report, brings evidence the report did not use, and asks the model to resolve the
conflict. "What a strong model should conclude" is my own analysis for the judges
— it is *not* a model answer, because the interactive RaptorX chat was not reachable
from this headless agent environment (login-gated UI); the questions are the
entry's primary contribution.

---

## Q1 — The JitoSOL premium anomaly (report §4, line: "JitoSOL $132.31 vs SOL $101.26, +30.7%")

> Your LST section prices JitoSOL at $132.31 against SOL at $101.26 — a 30.7%
> premium. JitoSOL is open-mint (deposit 1 SOL, mint 1:1 minus fees) and open-redeem
> (redeem to SOL). A persistent premium of that size should be arbitraged to roughly
> zero plus yield, because anyone can mint cheap JitoSOL and sell it into the premium.
> DefiLlama's Jito Liquid Staking TVL ($1.07B) matches CoinGecko's JitoSOL market cap
> ($1.053B on ~7.96M JitoSOL), so the *counts* agree — but the *price* is the outlier.
> Which data point is actually wrong: (a) CoinGecko's $132.31 JitoSOL price (in which
> case your premium-based conclusions collapse to a normal 1–3% yield-gap premium), or
> (b) the open-mint/open-redeem assumption (mint clogged, redemption queued, exchange
> listing mechanics that block mint-into-CEX arb)? What single on-chain check settles
> it — spot DEX JitoSOL/SOL pool invariant vs CoinGecko price, or mint-queue depth — and
> how does your risk assessment change if the true premium is ~0%?

**What a strong model should conclude:** The arb argument is tight: open mint + open
redemption caps the premium at ~mint cost + exchange spread (hours to reach parity).
So either CoinGecko's JitoSOL price is stale/broken for this asset (plausible: LST
pricing feeds on small-cap LSTs are noisy), or mint/redemption is genuinely constrained
(e.g., staker exit mechanics, a redemption queue, or the CEX listing not supporting
on-chain mint→withdraw). The decisive check is the JitoSOL/SOL CLMM pool invariant on
chain (p/sqrt(k) vs the two tokens' fair prices) plus live mint-queue depth. If the
pool invariant says parity, the premium is a data artifact and every "premium capture"
risk/return line in the report must be rewritten around a ~1–3% tip-yield gap instead.

---

## Q2 — FDV and the net-zero overhang (report §1/§5, line: "537.3M circulating of 1.0B total, FDV ≈ $418M, 1.86x MC")

> Your dilution risk is sized against a 1.0B total supply while circulating is 537.3M,
> giving an implied FDV of ~$418M (1.86x market cap). But Jito is in a net-zero
> governance regime. If the net-zero terms permanently void the unissued 463M JTO,
> then total supply is effectively 537M, FDV is meaningless, and your 1.86x dilution
> construct is overstating risk. If instead the 463M is a treasury/lockup with a
> release schedule, the honest question is the *release-weighted* overhang, not a
> 1.86x cap. Which DAO artifact settles this — the net-zero proposal text/tally or a
> treasury release schedule — and if it's a scheduled release, what multiple do you
> actually use, and does the "discount" framing survive?

**What a strong model should conclude:** Net-zero = issuance stops; the unissued
remainder is either (i) burned/voided or (ii) held by treasury with terms. The model
should name the exact artifacts to read (the governance vote text and any treasury
release schedule), then branch: if voided, re-state all multiples on 537M (MC is the
only meaningful denominator; "FDV" disappears); if scheduled, build a
release-weighted overhang curve (release dates × 463M) and discount accordingly —
the 1.86x flat cap is wrong in both cases. The report's risk ranking should move
"supply" from a structural overhang to a governance-terms question.

---

## Q3 — Venue concentration: organic flow or recycled volume (report §3, line: "Top-3 venues ≈ 69% of volume; GroveX alone 43.7%")

> Your venue table puts GroveX at $5.17M — 43.7% of JTO's global 24h volume — ahead of
> LBank ($1.93M) and Binance ($1.07M). Top-3 ≈ 69%. Two mutually exclusive readings:
> (a) JTO's real order flow genuinely concentrates in mid/long-tail venues (a venue
> risk you can size), or (b) the headline $11.8M is inflated by recycled/wash volume
> on one venue, and the honest "real" volume is only the Tier-1 residual. What depth
> test separates them — e.g., ±2% order-book depth at GroveX vs Binance, and the
> market impact of a $250K sell executed across top-3 vs top-10 venues — and if (b) is
> right, what does the real volume figure look like and what does that do to your
> liquidity conclusion?

**What a strong model should conclude:** Headline volume is a venue-weighted sum with no
per-venue integrity check, so a single recycled venue can dominate it. The discriminant:
if GroveX's ±2% depth is thin (≪ the $250K impact level) while its reported volume is
$5.17M, the volume/depth ratio is implausible for organic flow → reading (b). Real
volume ≈ sum of Tier-1 venues (Binance+OKX+Upbit+WhiteBIT ≈ $4–5M → vol/MC ≈ 2–3%,
the "thin mid-cap" baseline), and the liquidity conclusion should be "JTO is a thin,
venue-dependent asset; execute in tranches on Tier-1 venues; size stops by Tier-1
depth, not by headline volume."

---

## Q4 — The MEV cash-flow bridge to JTO (report §2, line: "tip pool accrues to stakers/validators; JTO has no direct fee cash flow")

> Your flywheel says Jito's MEV business monetizes through tips that flow to
> stakers/validators (the JitoSOL APR premium), while JTO is a governance token with
> no direct fee cash flow. Then the entire value bridge from the ~$1.07B JitoSOL
> business to JTO holders is *optionality*: a future governance act (fee switch,
> tip-redistribution, buyback) is what would convert staker cash flow into token
> cash flow. Is MC/TVL ≈ 0.21x a "cheap" signal or a "no-cash-flow" signal on that
> reading, and what specific governance artifact would you have to see to re-rate JTO
> from "infra option" to "cash-flow asset" — and at what pace/scale of that artifact
> (e.g., % of tips to buyback) does the re-rating actually change a multiple?

**What a strong model should conclude:** With tips accruing to stakers, JTO is priced
on optionality, so 0.21x MC/TVL is *not* a discount — it's a cash-flow-free multiple;
comparing it to cash-flow LST protocols would be category error. The re-rating
trigger is a governance vote that directs a material share of tips/revenue to JTO
(buyback/burn or staker→token fee switch); the model should quantify the threshold:
at ~$1.07B JitoSOL TVL with tip APR of a few percent, a 25–50% fee switch to buyback
is a meaningful JTO accretion vs the $224.6M cap — that's the scale at which the
"option" becomes a "cash-flow asset." Until then, JTO's floor is governance value and
the Solana ecosystem's MEV dominance.

---

## Why these four

- Each is **report-anchored** (a specific line in REPORT-JTO.md), **evidence-bringing**
  (DefiLlama TVLs, venue table, governance regime, on-chain arb mechanics — none used
  in the report's own numbers), and **resolvable** (names the exact check that
  separates the readings).
- Together they cover the report's four load-bearing claims: LST premium (§4),
  dilution (§1/§5), liquidity (§3), and token economics (§2) — the "better questions"
  that change at least one conclusion: premium → data artifact; 1.86x FDV →
  release-weighted or voided; 5.3% vol/MC → 2–3% real; 0.21x "cheap" → "no cash flow."
