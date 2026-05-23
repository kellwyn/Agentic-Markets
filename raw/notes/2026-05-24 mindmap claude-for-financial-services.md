# Mind map: Claude for Financial Services (GitHub)

> **Source kind:** mind map (image) provided by user 2026-05-24.
> **About:** Anthropic's "Claude for Financial Services" — a GitHub repo
> bundling vertical AI agents, skills, MCP connectors, and deployment
> templates targeted at financial services use cases.
> **Transcribed from image** — original lives in the conversation context;
> verify against the upstream repo if claims become load-bearing.

## Root: Claude for Financial Services (GitHub)

### Deployment Options
- Claude Cowork Plugin
- Claude Managed Agents API
- Claude for Microsoft 365

### Core Agents
- Pitch Agent
- Meeting Prep Agent
- Market Researcher
- Earnings Reviewer
- Model Builder
- Valuation Reviewer
- GL Reconciler
- KYC Screener

### Vertical Skill Bundles
- Financial Analysis (Core)
- Investment Banking
- Equity Research
- Private Equity
- Wealth Management
- Fund Admin & Ops

### Key Components
- Skills (Domain Expertise)
- Commands (Slash Actions)
- Connectors (MCP Servers)
- Cookbooks (Deployment Templates)

### MCP Data Providers
- S&P Global
- LSEG
- FactSet
- Morningstar
- Moody's
- PitchBook

### Repository Structure
- `plugins/`
- `managed-agent-cookbooks/`
- `scripts/`
- `claude-for-msft-365-install/`

---

## Notes from the user

(none — bare mind map dropped in)

## My read on what's interesting

- The product is **explicitly vertical**: not a horizontal "use Claude
  better" play. Each agent maps to a real banking/research/PE workflow.
- The "Skills + Commands + Connectors + Cookbooks" decomposition is the
  same decomposition Claude Code uses for its own extensibility — they're
  reusing infrastructure.
- The MCP Data Providers list is the **moat**: S&P, LSEG, FactSet, etc.
  are the same providers a real trading shop pays six figures a year for.
  Bundling them behind MCP is a serious distribution play.
