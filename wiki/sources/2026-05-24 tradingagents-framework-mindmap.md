---
type: source
created: 2026-05-24
updated: 2026-05-24
source_kind: note
source_path: raw/notes/2026-05-24 mindmap tradingagents-framework.md
tags: [area/agents, framework, langgraph, mcp/no, implementation]
---

# TradingAgents Framework — implementation view (mind map)

**Source:** mind map provided by user 2026-05-24, transcribed at
[[2026-05-24 mindmap tradingagents-framework]].
**About:** an operational view of the open-source TradingAgents framework
— covers concrete deployment choices the
[[2026-05-24 tauric-tradingagents-paper|Tauric paper]] does not.

## TL;DR
- Maps to the Tauric paper's 7-role architecture but **adds Research
  Manager and Portfolio Manager** roles, and refines Risk Management into
  Aggressive/Conservative/Neutral labels.
- Commits to a concrete stack:
  - **Orchestration:** LangGraph StateGraph + shared AgentState blackboard
  - **Tool layer:** `@tool` decorator (LangGraph/LangChain style)
  - **Output discipline:** Pydantic structured output
  - **Memory:** persistent decision memory + deferred reflection +
    SQLite checkpoint resume
  - **Model selection:** LLM Factory abstraction (Quick vs Deep tiers)
  - **Data:** vendor dispatcher across yfinance / Alpha Vantage / etc.
- Service-tier matrix: Free (Ollama + yfinance) → Freemium (Gemini +
  yfinance) → Paid (GPT-4 / Claude + Alpha Vantage).

## Key takeaways
- **The mind map is the engineering reality** that makes the paper
  runnable. "Agents debate in n rounds" (paper) becomes "LangGraph
  StateGraph with typed handoffs and SQLite checkpoints" (mind map).
- **Two-tier model selection** (Quick vs Deep) directly implements the
  paper's `gpt-4o-mini` for retrieval / `o1-preview` for reasoning split,
  abstracted behind a factory.
- **5-Tier Rating Parser** suggests a structured output schema for
  trader decisions — not in the paper. (Likely Strong Buy → Strong Sell,
  but verify in code.)
- **Service tiers explicitly include self-hosted Ollama** — the framework
  is designed to be runnable without paid API access, lowering the
  experimentation bar.

## Notable connections
- Sibling to [[2026-05-24 tauric-tradingagents-paper]] — same project,
  different layer of abstraction.
- The LangGraph commitment is in direct tension with
  [[Agentic AI System Course]]'s explicit anti-framework stance.
  Captured on [[LangGraph]] entity page.
- The `@tool` + Pydantic + checkpoint pattern is the standard kit for
  LangGraph-era multi-agent systems. Maps to
  [[Structured Agent Communication]] (typed inter-team handoffs) and
  [[Agent Role Specialization]] (each agent is a typed node).

## Open questions
- **Divergence from paper roles.** The paper has 7 roles ending in Fund
  Manager. The mind map adds Research Manager + Portfolio Manager. Is
  this:
  - (a) a fork/extension of the original framework,
  - (b) an updated version of the framework that postdates the paper,
  - (c) the mind-map author's reinterpretation?
  Verify against the actual repo before treating this as canonical.
- **"Deferred Reflection Loop"** — exact mechanism? (Reflection-driven
  agents in the related-work section of the paper map to FinMem / FinAgent
  layered memory. Is this the same idea?)
- **No evaluation in the mind map.** The framework's apparent
  productionization could overshadow the fact that the paper's
  performance evidence is weak (see [[Backtest Validity]]).

## Wiki updates made (this ingest)
- Created [[TradingAgents Framework]] entity (linked from both this and the paper)
- Created [[LangGraph]] entity
- Strengthened [[Agent Role Specialization]] with the expanded role set
- Strengthened [[Structured Agent Communication]] with the typed-handoff implementation pattern
