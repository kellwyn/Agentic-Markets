---
type: source
created: 2026-05-24
updated: 2026-05-24
source_kind: note
source_path: raw/notes/2026-05-24 mindmap claude-for-financial-services.md
tags: [area/agents, vendor/anthropic, vertical/finance, mcp]
---

# Claude for Financial Services (Anthropic GitHub bundle)

**Source:** mind map provided by user 2026-05-24, transcribed at
[[2026-05-24 mindmap claude-for-financial-services]].
**Origin (per mind map):** an Anthropic GitHub repository bundling
vertical AI agents, skills, MCP connectors, and deployment templates for
financial services.

## TL;DR
- Anthropic's vertical play for finance: not "use Claude better," but
  pre-built agents (Pitch, Meeting Prep, Earnings Reviewer, KYC Screener,
  …) targeting specific banker / analyst / PE workflows.
- Three deployment surfaces: Cowork plugin, Managed Agents API, M365.
- Decomposes into the same primitives Claude Code uses: **Skills**,
  **Commands**, **Connectors (MCP)**, **Cookbooks**.
- Bundled **MCP connectors to paid data providers**: S&P Global, LSEG,
  FactSet, Morningstar, Moody's, PitchBook. This is the moat.

## Key takeaways
- **Vertical agents over horizontal helpers.** Each Core Agent maps to a
  real role/task: Earnings Reviewer (sell-side analyst), GL Reconciler
  (controller), KYC Screener (compliance). The product wins by being
  opinionated about the workflow.
- **Vertical Skill Bundles** layer above Core Agents: Investment Banking,
  Equity Research, Private Equity, Wealth Management, Fund Admin & Ops.
  → Same underlying primitives, different opinionated configurations.
- **MCP is the substrate.** Six premium data providers behind MCP servers
  means Claude can call structured financial data without bespoke
  integration code. This is a distribution + moat play, not a UX flourish.
- **Cookbooks** = deployment templates → suggests Anthropic wants
  customers to fork/customize, not just consume.

## Notable connections
- The MCP layer connects to [[Model Context Protocol]] which also appears
  prominently in [[Agentic AI System Course]] (Ch.12–14).
- The vertical-agent-team idea overlaps with [[TradingAgents Framework]]
  but at a different abstraction: TradingAgents wires a *single*
  decision-making firm; Claude for Fin Services exposes *many independent*
  workflows that may or may not coordinate.
- "Skills + Commands + Connectors + Cookbooks" mirrors Claude Code's own
  extensibility primitives — Anthropic is dogfooding its own platform.

## Open questions
- Is the framework opinionated about *coordination* between agents (e.g.
  Pitch Agent + Market Researcher), or are they independent skills?
- How do the "Managed Agents API" deployments compare to running these
  agents locally via the plugin? Cost / latency / data residency
  implications.
- Are the data provider MCP connectors official partnerships, or
  community-built wrappers around their APIs?

## Wiki updates made (this ingest)
- Created [[Claude for Financial Services]] entity
- Created [[Model Context Protocol]] entity (bridged with course source)
- Updated [[overview]] working thesis to note vertical AI agent product play
