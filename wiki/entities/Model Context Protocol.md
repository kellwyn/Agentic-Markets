---
type: entity
created: 2026-05-24
updated: 2026-05-24
tags: [protocol, vendor/anthropic, tool-integration, mcp]
sources: ["[[2026-05-24 claude-for-financial-services]]", "[[2026-05-24 bryanyzhu-agentic-ai-course]]"]
confidence: low
---

# Model Context Protocol (MCP)

> An open protocol (Anthropic-origin, 2024) for connecting LLM agents to
> external data sources and tools via standardized "MCP servers."

## What it is

A client-server protocol where:

- **MCP servers** expose tools, resources, and prompts in a typed format.
- **MCP clients** (LLM hosts like Claude Desktop, Claude Code, Cursor)
  discover and call those servers without bespoke integration code.

The promise: write the integration once as an MCP server, every
MCP-aware client can use it.

## Why it shows up here

Two independent sources reference MCP prominently:

1. **[[Claude for Financial Services]]** ships MCP connectors to six
   premium data providers (S&P Global, LSEG, FactSet, Morningstar,
   Moody's, PitchBook). This is the **moat layer** of that product —
   pre-built bridges to data that would otherwise require separate
   commercial integrations.
2. **[[Agentic AI System Course]]** dedicates chapters 12–14 (External
   Surface block) to *connectors / MCP / skills / subagents* — i.e.
   MCP is treated as foundational vocabulary for production agents.

That two unrelated sources both put MCP at the center of "how agents
access the world" suggests it's becoming the de-facto integration
substrate, at least in the Anthropic ecosystem.

## When to use it

- Connecting LLM agents to data sources or tools you want reusable
  across hosts. ✅
- Building an MCP server for an internal API so multiple agent products
  can share it. ✅
- One-shot integration with a single LLM provider. ❌ — overhead exceeds
  benefit; use the provider's native tool-call format.

## Notable design choices

- **Typed schemas** for tools (similar to OpenAI function-calling /
  Anthropic tool-use but standardized across hosts).
- **Server-side state** — MCP servers can hold context across calls.
- **Resource model** — not just functions; servers can expose readable
  resources (files, URIs) the LLM can choose to fetch.

## Open questions

- Adoption outside the Anthropic ecosystem? OpenAI / Google have their
  own tool-use formats — is MCP becoming truly cross-vendor?
- Security model: how do MCP servers authenticate, and what's the
  surface area for prompt-injection via tool descriptions?
- Performance: each tool call is a round-trip; for high-frequency
  use cases the latency may dominate.

## Related

- The [[Claude for Financial Services]] MCP connector list (S&P / LSEG /
  FactSet / Morningstar / Moody's / PitchBook) is a roadmap of which
  premium data providers Anthropic has bridged.
- [[Structured Agent Communication]] — MCP's typed-schema discipline is
  the *external* analogue of structured handoffs *between* agents.
