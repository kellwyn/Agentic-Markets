# TradingAgents: Multi-Agents LLM Financial Trading Framework

> **Cite:** Xiao, Y., Sun, E., Luo, D., Wang, W. (2025). *TradingAgents:
> Multi-Agents LLM Financial Trading Framework.* arXiv:2412.20138v7
> [q-fin.TR], 3 Jun 2025. UCLA / MIT / Tauric Research.
> **Source URL:** https://arxiv.org/abs/2412.20138
> **Code:** https://github.com/TauricResearch/TradingAgents
> **Org:** https://tauric.ai
>
> **Source kind:** academic paper (PDF) attached to conversation 2026-05-24.
> Below is a markdown transcript of the key sections — for verbatim quotes
> always go back to the PDF.

---

## Abstract (verbatim)

> Significant progress has been made in automated problem-solving using
> societies of agents powered by large language models (LLMs). In finance,
> efforts have largely focused on single-agent systems handling specific
> tasks or multi-agent frameworks independently gathering data. However,
> the multi-agent systems' potential to replicate real-world trading firms'
> collaborative dynamics remains underexplored. TradingAgents proposes a
> novel stock trading framework inspired by trading firms, featuring
> LLM-powered agents in specialized roles such as fundamental analysts,
> sentiment analysts, technical analysts, and traders with varied risk
> profiles. The framework includes Bull and Bear researcher agents
> assessing market conditions, a risk management team monitoring exposure,
> and traders synthesizing insights from debates and historical data to
> make informed decisions. By simulating a dynamic, collaborative trading
> environment, this framework aims to improve trading performance.
> Detailed architecture and extensive experiments reveal its superiority
> over baseline models, with notable improvements in cumulative returns,
> Sharpe ratio, and maximum drawdown, highlighting the potential of
> multi-agent LLM frameworks in financial trading.

---

## Two stated limitations of existing systems (Sec. 1)

1. **Lack of Realistic Organizational Modeling** — most frameworks don't
   mirror real trading-firm structure; they focus narrowly on tasks
   disconnected from organizational workflow.
2. **Inefficient Communication Interfaces** — pure natural-language
   message-passing produces a "telephone effect": detail loss, state
   corruption as conversations lengthen, and retrieval-only coupling that
   breaks relational integrity.

These two limitations are the paper's leverage points.

---

## Architecture: 7 agent roles in 5 stages (Sec. 3)

> "TradingAgents defines seven distinct agent roles within a simulated
> trading firm: Fundamentals Analyst, Sentiment Analyst, News Analyst,
> Technical Analyst, Researcher, Trader, and Risk Manager."

The five stages of Figure 1:

1. **Analysts Team** — Fundamentals, Sentiment, News, Technical analysts
   concurrently gather information into specialized reports.
2. **Research Team** — Bullish and Bearish researchers debate over `n` rounds
   moderated by a facilitator, who selects a prevailing perspective.
3. **Trader** — Produces decision signal + detailed rationale report.
4. **Risk Management Team** — Risky / Neutral / Safe (Conservative) analysts
   debate over `n` rounds to adjust trade plan within risk constraints.
5. **Fund Manager** — Reviews risk discussion, finalizes trader's decision.

All agents use ReAct (Yao et al. 2023): reasoning + acting interleaved.

---

## Communication protocol (Sec. 4.1–4.2) — *the most novel part*

Hybrid structured + natural-language design:

- **Structured documents** (typed reports) for handoffs between teams.
- **Natural language dialogue** *only* during intra-team debates
  (researcher debate, risk debate). Conversation state is logged as a
  structured entry in the global agent state.

> "Each role only extracts or queries the necessary information, processes
> it, and returns a completed report."

This is the answer to the "telephone effect" — natural language is
contained inside debate sub-protocols; everything that crosses team
boundaries is structured.

---

## Backbone LLMs (Sec. 4.3)

- **Quick-thinking** (`gpt-4o-mini`, `gpt-4o`) — summarization, data
  retrieval, table→text.
- **Deep-thinking** (`o1-preview`) — decision making, evidence-based
  report writing, multi-round reasoning.
- All analyst nodes use deep models; tool/API retrieval uses quick models;
  researchers and traders use deep models.
- GPU-free: "relying only on API credits."
- Backbone is exchangeable (any locally hosted or API-accessible model).

---

## Experiments (Sec. 5–6)

- **Window:** 2024-01-01 → 2024-03-29 (~3 months).
- **Tickers:** AAPL, GOOGL, AMZN, MSFT, META.
- **Baselines:** Buy-and-Hold, MACD, KDJ+RSI, ZMR, SMA.
- **Metrics:** CR (cumulative return), ARR (annualized), SR (Sharpe), MDD.
- **Compute footprint:** ~11 LLM calls + 20+ tool calls per prediction.

### Results table (verbatim, Table 1)

| Ticker | Strategy | CR% | ARR% | SR | MDD% |
|---|---|---|---|---|---|
| AAPL | B&H | -5.23 | -5.09 | -1.29 | 11.90 |
| AAPL | MACD | -1.49 | -1.48 | -0.81 | 4.53 |
| AAPL | KDJ&RSI | 2.05 | 2.07 | 1.64 | 1.09 |
| AAPL | ZMR | 0.57 | 0.57 | 0.17 | 0.86 |
| AAPL | SMA | -3.2 | -2.97 | -1.72 | 3.67 |
| **AAPL** | **TradingAgents** | **26.62** | **30.5** | **8.21** | **0.91** |
| GOOGL | TradingAgents | 24.36 | 27.58 | 6.39 | 1.69 |
| AMZN | TradingAgents | 23.21 | 24.90 | 5.60 | 2.11 |

### Author's own caveat (verbatim footnote)

> "We benchmarked TradingAgents over 3 months due to intensive LLM and
> tool use (11 LLM calls & 20+ tool calls/prediction). The highest Sharpe
> Ratio exceeds our expected empirical range (SR above 2 – very good,
> above 3 – excellent). … We believe the exceptionally high SR resulted
> from the phenomenon that there were few pullbacks in TradingAgents
> during that period. We report results as they are in our experiments
> faithfully. Future work will optimize LLM reasoning & tool use to enable
> longer backtesting under limited budgets."

**This is honest but limiting.** SR of 8.21 over 3 months on a single
period is not robust evidence. The result is *suggestive*, not *validated*.

---

## Related work summary (Sec. 2)

Three lineages:
1. **LLMs as financial assistants** — BloombergGPT, FinGPT, FinMA, Fin-T5,
   Instruct-FinGPT. Domain-adapted via fine-tuning or pretraining.
2. **LLMs as traders** — three sub-lineages:
   - News-driven (Lopez-Lira & Tang 2023; FinGPT-Forecaster)
   - Reasoning-driven (FinMem, FinAgent, TradingGPT, Xing 2024)
   - RL-driven (SEP, PPO with LLM embeddings)
3. **LLMs as alpha miners** — QuantAgent, AlphaGPT (writer + judge loop).

TradingAgents positions itself as a reasoning-driven multi-agent
framework with explicit organizational mimicry.

---

## Explainability claim (Sec. 6.1.4)

Decisions are communicated in natural language with full ReAct logs
(thoughts + tool calls + observations + final report). The paper provides
a sample day's full log for AAPL in Appendix S1.4, showing:
- Market analyst's RSI/ADX/Bollinger/MACD/VWMA/ATR/Supertrend/CCI report
- News analyst's macro digest (Trump return, CPI, US-China, TSMC subsidy)
- Sentiment analyst's Reddit + EODHD sentiment scores by date
- Fundamentals analyst's metrics dump
- Bull vs Bear researcher debate
- Risky / Safe / Neutral risk debate
- Fund manager final BUY recommendation with rationale

The transcript reads coherently — this is the genuine differentiator
over deep-learning trading.

---

## Open questions raised by this paper

- Survivorship and selection bias in choosing AAPL/GOOGL/AMZN/MSFT/META —
  large-cap tech in early 2024 was a uniformly favorable regime.
- The 3-month window precludes regime analysis (compare to
  [[2026-05-24 mindmap market-regimes|Market Regimes]] which calls for
  multi-year / multi-regime evaluation).
- Cost: ~11 LLM calls + 20 tool calls per *daily* decision per ticker —
  for a portfolio of 50 names this is ~3,500 calls/day. Live deployment
  economics need their own analysis.
- No mention of execution / slippage / market impact. Decisions are
  evaluated at close prices.
- The Bull/Bear debate is run with the *same* LLM playing both roles.
  Genuine independence is unclear — see also Du et al. 2023 on multi-agent
  debate.

---

## My read on what's worth filing back

- **Concept page: [[Multi-Agent LLM Trading Systems]]** — this paper is
  the canonical reference.
- **Concept page: [[Bull-Bear Debate]]** — paper formalizes it with `n`
  rounds + facilitator selection.
- **Concept page: [[Structured Agent Communication]]** — the
  structured-doc-with-NL-debate-pockets pattern is reusable across domains.
- **Concept page: [[Agent Role Specialization]]** — 7-role taxonomy.
- **Concept page: [[Backtest Metrics]]** — CR, ARR, SR, MDD formulas
  (Sec S1.2 equations).
- **Entity page: [[TradingAgents Framework]]** — the actual codebase.
- **Entity page: [[Tauric Research]]** — the lab.
- **Entity page: [[ReAct Prompting]]** — the prompting framework all
  agents use.
