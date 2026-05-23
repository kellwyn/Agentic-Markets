---
type: meta
created: 2026-05-24
updated: 2026-05-24
tags: [index, navigation]
---

# Index

Content catalog. Maintained by Claude on every ingest. Organized by category,
with a one-line summary per page. Read this first when answering a query.

> Counts: 5 sources · 6 entities · 6 concepts · 0 analyses · 0 journal entries.

## Overview & meta
- [[overview]] — living synthesis: agentic AI for markets, opening thesis after first ingest
- [[log]] — chronological record of ingests, queries, lints

## Sources

### Papers
- [[2026-05-24 tauric-tradingagents-paper]] — *Tauric TradingAgents (arXiv 2412.20138v7):* multi-agent LLM trading framework mimicking a trading firm; 7 roles, hybrid structured + NL communication, 3-month backtest with author-flagged caveats

### Articles / repos
- [[2026-05-24 bryanyzhu-agentic-ai-course]] — 22-chapter framework-agnostic course on agentic AI systems; Karpathy-pattern cousin to this wiki

### Notes / mind maps
- [[2026-05-24 claude-for-financial-services]] — Anthropic's vertical product: pre-built finance agents + Skills/Commands/Connectors/Cookbooks + MCP to S&P/LSEG/FactSet/Morningstar/Moody's/PitchBook
- [[2026-05-24 market-regimes-framework]] — three-pillar (macro / structural-regulatory / micro) framework, India-flavored, explicit on hindsight bias
- [[2026-05-24 tradingagents-framework-mindmap]] — implementation view of TradingAgents Framework: LangGraph + Pydantic + SQLite + LLM Factory + service tiers

## Entities

### Frameworks & products
- [[TradingAgents Framework]] — open-source multi-agent stock-trading system from Tauric Research; LangGraph + Pydantic implementation of the arXiv paper
- [[Claude for Financial Services]] — Anthropic's vertical agent bundle (Pitch / Earnings / KYC / GL Reconciler / …) with MCP connectors to premium data providers
- [[LangGraph]] — graph-based multi-agent orchestration framework; the de-facto LangChain-ecosystem choice; TradingAgents commits to it
- [[Model Context Protocol]] — typed protocol for LLM agents to access external tools/data; substrate of both Claude for Fin Services and the bryanyzhu course Ch.12

### Research groups & curricula
- [[Tauric Research]] — UCLA / MIT lab; authors of the TradingAgents paper and codebase
- [[Agentic AI System Course]] — bryanyzhu's 22-chapter skeleton course; explicitly framework-agnostic; sits in productive tension with TradingAgents' LangGraph commitment

## Concepts

### Agent architecture
- [[Multi-Agent LLM Trading Systems]] — umbrella concept: role-specialized LLM societies that mimic trading firms
- [[Agent Role Specialization]] — decomposing into narrow-role agents; the 7-role Tauric taxonomy + the vertical-product alternative (Claude for Fin Services)
- [[Bull-Bear Debate]] — dialectical sub-pattern with `n`-round NL debate + facilitator selection; the only place NL is allowed inside the Tauric protocol
- [[Structured Agent Communication]] — typed-doc handoffs between teams, natural language quarantined inside debates; the anti-telephone pattern

### Markets
- [[Market Regimes]] — three-pillar framework for regime identification; macro + structural/regulatory + micro
- [[Backtest Validity]] — skeptical lens on agentic-trading evaluations; regime-dependence, curated universes, short windows, author-flagged but ignored caveats

## Analyses
_None yet — file query answers here when they're worth keeping._

## Journal
_None yet — personal trade notes and observations._

---

## How to read this file (for Claude)
1. When a user asks a question, scan this catalog top-to-bottom for relevant
   pages by category. The one-liners are written to make relevance obvious.
2. Drill into candidate pages and follow `[[wikilinks]]`.
3. After answering or ingesting, update entries here whose one-liner no
   longer matches the page content.
4. Keep the count line at the top accurate.
