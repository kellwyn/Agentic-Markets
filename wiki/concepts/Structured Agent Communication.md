---
type: concept
created: 2026-05-24
updated: 2026-05-24
tags: [area/agents, multi-agent, protocol, design-pattern]
sources: ["[[2026-05-24 tauric-tradingagents-paper]]", "[[2026-05-24 tradingagents-framework-mindmap]]", "[[2026-05-24 bryanyzhu-agentic-ai-course]]"]
confidence: medium
---

# Structured Agent Communication

> The design pattern of having agents exchange typed, structured
> documents instead of free-form natural-language messages — to prevent
> the "telephone effect" that degrades pure-NL multi-agent systems.

## Summary

Pure natural-language message passing between agents has a well-known
failure mode: as conversations lengthen, earlier details get distorted
or forgotten, agent state corrupts, and retrieval-based context lookup
breaks the relational integrity of the information.

The fix: **structured documents (typed reports) across team boundaries,
with natural language quarantined inside bounded sub-protocols** like
debates. Each agent extracts/queries only the necessary fields, processes
them, and returns a typed report that downstream agents can rely on as
a contract.

Canonical reference:
[[2026-05-24 tauric-tradingagents-paper|Tauric §4.1–4.2]].
Implementation: [[TradingAgents Framework]] uses Pydantic models for the
typed reports and a shared `AgentState` blackboard per
[[2026-05-24 tradingagents-framework-mindmap]].

## Key claims

- **"Telephone effect" is the load-bearing failure mode.** Quote from
  the paper:
  > "Pure natural language communication can resemble a game of
  > telephone — over multiple iterations, initial information may be
  > forgotten or distorted due to context length limitations and an
  > overload of text that obscures critical earlier details."
  → [[2026-05-24 tauric-tradingagents-paper]]
- **Hybrid > pure-structured or pure-NL.** Both extremes fail.
  Pure-structured loses the dialectical reasoning Bull-Bear debate
  needs; pure-NL corrupts state. The Tauric hybrid runs structured
  handoffs by default and *quarantines* NL inside debate sub-protocols,
  recording the debate result as structured state.
- **Pydantic / JSON Schema is the natural enforcement tool.** A typed
  report schema is checkable, and the LLM can be re-prompted on a
  schema violation. → [[TradingAgents Framework]] mindmap.
- **MCP is the external analogue.** Where this concept governs agent-
  to-agent communication, [[Model Context Protocol]] governs agent-to-
  tool communication using the same typed-schema discipline. The
  [[Agentic AI System Course]] Ch.12–14 (Connectors / MCP / Subagents)
  treats them as the same family of patterns.

## Mechanics (Tauric variant)

| Stage | Communication style | Why |
|---|---|---|
| Analyst → shared state | Typed report per analyst | Concise, queryable, no telephone |
| Researcher debate | Natural language, `n` rounds | Dialectical reasoning needs free-form argument |
| Researcher → Trader | **Typed** prevailing-perspective entry written by facilitator | Debate result is contract-grade |
| Trader → Risk Management | Typed decision + rationale report | Risk team operates on the typed proposal, not the debate text |
| Risk debate | Natural language, `n` rounds | Same justification as research debate |
| Risk → Fund Manager | Typed adjusted proposal | Final approval operates on contract |

The pattern: **NL only where dialectical reasoning is the point;
everything else is typed.**

## Known failure modes

- **Over-rigid schemas.** If the typed report omits a field the LLM
  surfaced as important, that information is lost. Schemas need open
  text fields for novel observations.
- **Schema drift.** As agents evolve, schemas need versioning; mismatched
  versions in the same graph are silent failures.
- **Validation bypass.** Some LLMs hallucinate schema-conformant garbage;
  validation catches type errors but not semantic errors.

## Open questions

- Schema versioning strategies in long-running agent graphs.
- Trade-offs between Pydantic models (Python-coupled) vs JSON Schema
  (language-agnostic) vs Protobuf (binary, schema-evolution-friendly).
- Does the typed-report discipline degrade performance on tasks where
  the LLM's free-text insight outperforms structured output?

## Related

- [[Bull-Bear Debate]] — the canonical "NL is contained here" example.
- [[Model Context Protocol]] — external analogue (typed agent-tool comms).
- [[Multi-Agent LLM Trading Systems]] — the system-level pattern this
  enables.
- [[TradingAgents Framework]] / [[LangGraph]] — concrete implementation.
