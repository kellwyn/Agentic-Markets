---
type: concept
created: 2026-05-24
updated: 2026-05-24
tags: [area/markets, backtest, evaluation, skepticism]
sources: ["[[2026-05-24 tauric-tradingagents-paper]]", "[[2026-05-24 market-regimes-framework]]"]
confidence: medium
---

# Backtest Validity

> A backtest is valid only to the extent it tells you something about
> the strategy's behavior under conditions you actually care about.
> Strong numerical results in a single regime, on a curated universe,
> over a short window, are *suggestive* — they are not *evidence*.

## Summary

Most published agentic-trading results suffer from at least one of:

1. **Short windows** — months, not years.
2. **Curated universes** — selected large-cap names that were favorable.
3. **Single regime** — backtest spans one macro/micro state.
4. **No execution modeling** — decisions evaluated at close prices,
   no slippage or market impact.
5. **No transaction costs** — particularly damaging at high turnover.
6. **Self-flagged caveats nobody reads** — authors note the limitation
   in a footnote and the headline number gets cited anyway.

The [[2026-05-24 tauric-tradingagents-paper|Tauric TradingAgents paper]]
is the canonical example here: it reports CR=26.62% / SR=8.21 / MDD=0.91
on AAPL over 3 months in early 2024, and the authors themselves write
in a footnote:

> "The highest Sharpe Ratio exceeds our expected empirical range
> (SR above 2 – very good, above 3 – excellent). … We believe the
> exceptionally high SR resulted from the phenomenon that there were
> few pullbacks in TradingAgents during that period."

That caveat is honest. The headline number citing it as "novel
multi-agent framework beats baselines" hides the qualification.

## Key claims

- **Regime-dependence is the strongest critique of single-window
  backtests.** A 3-month window on big-tech in early 2024 spans one
  regime. The same strategy in a different regime (high-vol 2022, COVID
  2020, sideways 2015) may produce opposite results. See
  [[Market Regimes]].
- **Curated universe ≈ survivorship bias.** AAPL, GOOGL, AMZN, MSFT,
  META in 2024 were uniformly favorable; this is *exactly* the universe
  where any reasonable long-only signal makes money.
- **SR > 3 in any short window is suspicious.** Empirically, sustained
  Sharpe > 2 is excellent. SR=8.21 over 3 months almost certainly
  reflects favorable regime + small sample, not signal quality.
- **The authors' caveat does not propagate.** When papers cite this
  work downstream, the headline numbers get reused without the
  footnote. The wiki should preserve the footnote.

## What a more-valid backtest looks like

| Dimension | Weak | Stronger |
|---|---|---|
| Window | 3 months | 5+ years, multiple regimes |
| Universe | 5 hand-picked big-caps | Full investable universe with delisting handled |
| Regime coverage | One | At least one of each: trending, mean-reverting, high-vol, low-vol |
| Execution | Close-price fills | Realistic fills with slippage + market impact |
| Costs | Zero | Per-trade commission + spread + borrow cost on shorts |
| Variance | Single backtest | Walk-forward + bootstrap + cross-validation |
| Robustness | Headline metric only | Sensitivity analysis on each free parameter |

## Common confusions

- **"Out-of-sample"** in many papers means *paper-authored after the
  data ended* but the model designers had years to see how 2024 played
  out before publishing. Real OOS = data that *did not exist* when the
  model was specified.
- **Per-asset returns ≠ portfolio returns.** A multi-agent system that
  picks AAPL well in one window says nothing about portfolio
  construction at 50+ names.
- **High Sharpe with low drawdown** is the *exact pattern* you'd expect
  from a strategy that lucky-traded a low-pullback window. It's not
  evidence of skill; it's evidence of a short benchmark.

## Open questions

- What's the minimum evaluation regime for an agentic trading system to
  be considered seriously? Multi-regime + multi-asset-class + realistic
  costs is the obvious answer, but no published agentic system meets it.
- **Cost-of-evidence.** Tauric's setup is ~11 LLM + 20 tool calls per
  daily decision per ticker. A 5-year, 50-name backtest at that rate is
  ~10M+ LLM calls. The cost wall is non-trivial — explains the short
  windows.

## Related

- [[Market Regimes]] — the framework for thinking about *which*
  regime(s) a backtest covered.
- [[Multi-Agent LLM Trading Systems]] — the umbrella concept this
  skepticism applies to.
- [[Tauric Research]] / [[TradingAgents Framework]] — the canonical
  case study for the skepticism, including its own honest caveat.
