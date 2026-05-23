---
type: concept
created: 2026-05-24
updated: 2026-05-24
tags: [area/markets, regimes, macro, regulatory, microstructure]
sources: ["[[2026-05-24 market-regimes-framework]]"]
confidence: medium
region: IN
---

# Market Regimes

> A market regime is a sustained, measurable structural state of a market
> — not a one-off spike. Identifying which regime you're in is upstream
> of strategy selection: the same edge can be profitable in one regime
> and ruinous in another.

## Summary

The three-pillar framework captured in
[[2026-05-24 market-regimes-framework|the regime mindmap]] decomposes
regime identification into:

1. **Macroeconomic Pillar** — what conditions is the economy in?
2. **Structural / Regulatory Pillar** — what rules govern the market?
3. **Micro / Market Structure Pillar** — what is price doing, and who
   is trading?

A regime is defined by:
- **Time frame** (intraday / daily / weekly / yearly) — same word
  ("trending regime") means different things at different scales.
- **Persistence** — sustained change, not a single-day spike.
- **Measurable parameters** — quantifiable features per pillar, not
  vibes.

The framework is India-flavored (SEBI, India VIX, FII/DII, T+1, STT,
ASM/GSM) but the pillar structure generalizes.

## Three pillars

### Pillar 1 — Macroeconomic
- **Interest rates & inflation** — real rates, hurdle rates above which
  equities become unattractive vs bonds.
- **Institutional flows** — FII (foreign institutional) selling vs DII
  + retail absorption. Emerging-market alternatives as substitute.
- **Currency strength.**
- **Commodities** — crude oil as the canonical macro input for India.
- **Structural macro shifts** — Quantitative Easing (QE) era,
  1991 Indian economic liberalization.

### Pillar 2 — Structural / Regulatory
- **Taxation** — long-term capital gains (LTCG) tax regime,
  Securities Transaction Tax (STT) revisions.
- **Operational changes** — pre-open session, T+1 settlement cycle.
- **Leverage regimes** — peak margin rules constrain intraday positioning.
- **Product evolution** — weekly options, index expansion.
- **Regulatory oversight** — SEBI as the regulator; ASM/GSM
  (Additional / Graded Surveillance Measures) frameworks.

### Pillar 3 — Micro / Market Structure
- **Technical indicators** — 200-day moving average; distance from
  all-time highs.
- **Volatility** — realized vs implied; India VIX as the canonical
  implied-vol gauge.
- **Market breadth.**
- **Factor-based rotation** — value vs momentum vs growth.
- **Market-cap rotation** — small vs mid vs large cap.

## Key claims

- **Regulation belongs in regime analysis.** A change to T+1 settlement
  or a tightening of peak margin rules is a regime change, not a
  microstructure footnote.
- **Time frame matters as much as direction.** "Trending up" daily ≠
  "trending up" yearly; strategies that work on one don't work on the
  other.
- **Hindsight bias is the practical killer.** Frameworks read cleanly
  ex-post and are nearly useless ex-ante. This is named explicitly in
  the source — "navigation skills vs analysis" is a separate skill from
  the framework itself.

## Open questions

- How are the pillars *operationalized*? Specific indicators per pillar
  (e.g. "real rates < -1% defines accommodative macro regime")?
- Where does liquidity at the microstructure level (spreads, depth,
  order-book imbalance) sit? Not obviously in Pillar 3.
- Source attribution unknown.
- Does this framework generalize to FX, commodities, crypto, or is it
  specifically equity-shaped?
- **Bridge to multi-agent systems.** None of the agentic frameworks
  ingested so far ([[TradingAgents Framework]],
  [[Claude for Financial Services]]) explicitly model regime as input
  to their decision pipelines. Integrating regime awareness into a
  [[Multi-Agent LLM Trading Systems|multi-agent system]] is an open
  design problem.

## Why this matters here

The Tauric paper backtests on 3 months of large-cap US tech in early
2024 — a single regime. The reported SR=8.21 is uninterpretable without
specifying *which regime* it was achieved in. See [[Backtest Validity]].

## Related

- [[Backtest Validity]] — regime-dependence is the strongest critique
  of single-window backtests.
- [[Multi-Agent LLM Trading Systems]] — where regime-awareness should
  but doesn't yet plug in.
