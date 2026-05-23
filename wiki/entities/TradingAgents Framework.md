---
type: entity
created: 2026-05-24
updated: 2026-05-24
tags: [framework, multi-agent, finance, langgraph, open-source]
sources: ["[[2026-05-24 tauric-tradingagents-paper]]", "[[2026-05-24 tradingagents-framework-mindmap]]"]
confidence: medium
---

# TradingAgents Framework

> An open-source multi-agent LLM framework for stock trading, simulating
> a trading firm's organizational structure. Maintained by [[Tauric Research]].

## What it is

A LangGraph-based Python framework where specialized LLM agents
(analysts, researchers, traders, risk managers, fund manager) collaborate
to produce daily Buy/Sell/Hold decisions for individual stocks. Inspired
by — and accompanied by — the academic paper at
[[2026-05-24 tauric-tradingagents-paper|arXiv 2412.20138]].

Repo: https://github.com/TauricResearch/TradingAgents.

## Architecture

Per the [[2026-05-24 tauric-tradingagents-paper|paper]] (canonical) and
[[2026-05-24 tradingagents-framework-mindmap|implementation mindmap]]:

**Stages** (the paper's 5; mindmap expands some):
1. **Analyst Team** — Market (technical), Social/Sentiment, News,
   Fundamentals. Concurrent, independent reports.
2. **Researcher Team** — Bull vs Bear, `n`-round debate facilitated by
   a moderator that selects the prevailing position. See [[Bull-Bear Debate]].
3. **Management / Trading** *(mindmap-only role labels)* — Research
   Manager, Trader, Portfolio Manager. The paper has Trader only;
   Research Manager and Portfolio Manager appear in the mindmap.
   → **Divergence flagged**, verify against the upstream repo.
4. **Risk Management Team** — Aggressive / Conservative / Neutral
   analysts debate in `n` rounds.
5. **Fund Manager** — finalizes the trade decision.

## Notable design choices

| Choice | Where it appears | Why it matters |
|---|---|---|
| **LangGraph StateGraph** | mindmap | Concrete orchestration commit; turns the paper's abstract "n-round debate" into typed nodes + edges |
| **Shared AgentState blackboard** | mindmap | All agents read/write a single typed dict — avoids message-passing leakage |
| **Pydantic structured output** | mindmap | Inter-team handoffs are typed reports, not free text — implements [[Structured Agent Communication]] |
| **LLM Factory (Quick vs Deep)** | mindmap (impls paper §4.3) | Cost lever: `gpt-4o-mini` for retrieval, `o1-preview` (or equiv) for reasoning |
| **SQLite checkpoint resume** | mindmap | Restart from a failed run; LangGraph-native |
| **5-Tier Rating Parser** | mindmap | Structured trader-decision output (likely SB/B/H/S/SS — verify) |
| **Vendor dispatcher** | mindmap | Pluggable data source: yfinance, Alpha Vantage, etc. |
| **ReAct prompting** | paper §3 (end) | Every agent interleaves reasoning + tool calls |

## When to use it

- **Educational / research.** Reproducing or extending the org-mimicry
  pattern for academic comparison. ✅
- **As a reference implementation.** Reading the code to see how the
  paper's protocol becomes a LangGraph state machine. ✅
- **Production trading.** ❌ — the paper's evaluation is one short window
  on five large-cap names in a uniformly favorable regime; the SR=8.21
  result is unreplicated and the authors themselves flag it. See
  [[Backtest Validity]] and [[Market Regimes]].

## Distinct from

- The **academic paper** ([[2026-05-24 tauric-tradingagents-paper]]) —
  the paper is the architectural spec; this entity is the codebase.
- **[[Claude for Financial Services]]** — vertical *product* (Anthropic)
  vs vertical *framework* (Tauric). Different abstraction layers,
  different go-to-market.

## Open questions

- Confirm role list against the actual `main` branch. The mindmap's
  Research/Portfolio Manager additions need verification.
- What's the 5-tier rating schema exactly?
- Is there an evaluation harness in the repo, or is the backtest code
  paper-only?
