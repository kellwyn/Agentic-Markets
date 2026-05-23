---
type: meta
created: 2026-05-24
updated: 2026-05-24
tags: [overview, synthesis]
confidence: low
---

# Overview

The living synthesis. What does this wiki currently believe about
**agentic AI applied to markets**? Rewritten as the wiki evolves.

> **Status:** post first ingest (5 sources). Working thesis is thin but
> directional — substantial gaps in both backtest evidence and
> regime-aware design remain.

## Working thesis (post-ingest 1)

After the first batch of sources, the picture forming is:

1. **There is a real and growing class of "multi-agent LLM trading
   systems"** — frameworks where role-specialized agents (analysts,
   researchers, traders, risk managers) collaborate to make trading
   decisions. The
   [[2026-05-24 tauric-tradingagents-paper|Tauric TradingAgents paper]]
   + [[TradingAgents Framework]] codebase are the canonical reference.
2. **Two distinct go-to-markets** for agentic finance products are
   visible: open-source research frameworks (Tauric) and vertical
   commercial bundles ([[Claude for Financial Services]]). They
   operate at different abstraction layers — pipeline-with-single-
   decision vs service-catalog-of-workflows. See
   [[Agent Role Specialization]].
3. **Common substrate is emerging:** LangGraph for orchestration,
   Pydantic for typed handoffs, [[Model Context Protocol|MCP]] for
   tool/data access, SQLite for checkpointing. The
   [[Agentic AI System Course]] documents this stack-agnostically; the
   [[TradingAgents Framework]] commits to it concretely. Both are right.
4. **Backtest evidence is weak across the board.** The strongest
   published result (Tauric SR=8.21) comes with the authors' own
   caveat that the metric exceeds their expected empirical range, on a
   3-month window in a single regime. See [[Backtest Validity]].
5. **Regime awareness is missing.** None of the ingested agentic
   frameworks model market regime as input. The
   [[Market Regimes]] framework is well-developed on the markets side
   but unintegrated with the agent designs. This is an open design
   problem.

## Active research threads
- **Verify TradingAgents Framework role list against the upstream
  repo** — the [[2026-05-24 tradingagents-framework-mindmap|mindmap]]
  adds Research Manager + Portfolio Manager roles not in the paper.
- **Bridge [[Market Regimes]] into [[Multi-Agent LLM Trading Systems]]
  design** — how would a "Regime Analyst" role fit into the Tauric
  taxonomy?
- **Cost-of-evidence problem** — multi-year multi-regime backtests at
  ~30 LLM+tool calls per daily decision per ticker are economically
  prohibitive. What's the cheapest valid evaluation?

## Settled claims (multiply supported, no source contradicts)
- **Pure NL message-passing between agents corrupts state** ("telephone
  effect"). Hybrid structured + NL communication beats both extremes.
  → [[Structured Agent Communication]]
- **The Karpathy meta-pattern (skeleton + AI muscles) generalizes.**
  It works for personal wikis, courses ([[Agentic AI System Course]]),
  and probably product specs.
- **Quick / Deep model-tier split is a cost lever**, not just a quality
  lever. → [[2026-05-24 tauric-tradingagents-paper]] §4.3 →
  [[TradingAgents Framework]] LLM Factory.

## Open contradictions
- **Framework commitment vs framework agnosticism.**
  [[Agentic AI System Course]] explicitly refuses to name a stack.
  [[TradingAgents Framework]] hard-commits to LangGraph + Pydantic.
  Both positions are defensible; the wiki preserves the tension.

## Adjacent areas (not yet covered)
- **India-specific regulation entities** (SEBI, ASM/GSM, T+1, STT,
  India VIX). Present in [[Market Regimes]] but no dedicated pages yet.
- **Premium data providers** (S&P Global, LSEG, FactSet, Morningstar,
  Moody's, PitchBook). Listed in [[Claude for Financial Services]] but
  no dedicated entity pages.
- **Reference agentic systems** (OpenCode, Hermes, OpenClaw, Paperclip)
  mentioned by [[Agentic AI System Course]] but unread.
- **Alternative orchestration frameworks** (CrewAI, AutoGen, Pydantic AI).
- **Execution / slippage / market impact modeling** — absent from all
  ingested agentic frameworks; an obvious next research direction.
- **Single-agent baselines** — FinMem, FinAgent, FinGPT, BloombergGPT
  referenced in Tauric §2 but unread.
