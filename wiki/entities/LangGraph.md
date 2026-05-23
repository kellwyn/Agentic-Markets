---
type: entity
created: 2026-05-24
updated: 2026-05-24
tags: [framework, orchestration, langchain-ecosystem]
sources: ["[[2026-05-24 tradingagents-framework-mindmap]]"]
confidence: low
---

# LangGraph

> A graph-based orchestration framework for multi-agent LLM systems,
> built on LangChain. Models agent workflows as a `StateGraph` of typed
> nodes with shared state.

## What it is

LangGraph (https://github.com/langchain-ai/langgraph) provides:

- **StateGraph** — a directed graph where each node is a function (often
  an LLM call or tool invocation) and edges define control flow.
- **Shared state object** (typed dict / Pydantic model) that nodes
  read from and write to — the "blackboard" pattern.
- **Checkpointing** — durable state via SQLite / Postgres so a run can
  resume after failure.
- **Subgraphs** — nested state machines for composition.

## Why it shows up here

[[TradingAgents Framework]] commits to LangGraph as its orchestration
layer (per the [[2026-05-24 tradingagents-framework-mindmap|mindmap]]).
Specifically:

- The "n-round Bull/Bear debate" is a subgraph with a loop edge.
- Risk debate (Risky/Conservative/Neutral) is another subgraph.
- Inter-team handoffs are typed reports stored in the shared AgentState.

This makes LangGraph the de-facto orchestration choice for the
paper-to-implementation mapping in
[[2026-05-24 tauric-tradingagents-paper|Tauric's paper]].

## Tension with framework-agnostic guidance

[[Agentic AI System Course]] explicitly refuses to name a stack —
"the course never says use LangChain or use Pydantic AI." But its
own coordination chapters (Ch.09–11: planning → multi-agent delegation
→ the harness) describe patterns that LangGraph implements directly.

Most production multi-agent systems we encounter end up framework-coupled
even when their *design talk* stays agnostic. Worth keeping in mind
when reading new sources: claims about "framework-agnostic patterns"
are easy to make and hard to live with.

## When to consider it

- Building a multi-agent system where typed inter-node handoffs and
  durable state matter. ✅
- Loose hierarchical workflows (planner → workers → critic). ✅
- Single-agent ReAct loop. ❌ — overkill; use LangChain's basic agent
  primitives or roll your own loop (per
  [[Agentic AI System Course]] Ch.01–02).

## Open questions

- How does LangGraph compare to alternatives we haven't ingested yet
  (CrewAI, AutoGen, Pydantic AI workflows)?
- Production runtime maturity — has anyone built a serious commercial
  system on it?
- Memory management at scale (long-running graphs, large state objects).
