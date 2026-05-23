---
type: entity
created: 2026-05-24
updated: 2026-05-24
tags: [product, vendor/anthropic, vertical/finance, mcp]
sources: ["[[2026-05-24 claude-for-financial-services]]"]
confidence: low
---

# Claude for Financial Services

> Anthropic's vertical agent product for financial services — a GitHub
> bundle of pre-built agents, skills, MCP connectors, and deployment
> templates targeting banker / analyst / PE / wealth-management workflows.

## What it is

A productized set of agents and skills layered on top of Claude, shipped
as a GitHub repo containing:

- `plugins/` — Cowork plugin code
- `managed-agent-cookbooks/` — templates for the Managed Agents API
- `scripts/` — utilities
- `claude-for-msft-365-install/` — M365 integration installer

Three deployment surfaces:
- **Claude Cowork Plugin** — desktop/IDE integration
- **Claude Managed Agents API** — Anthropic-hosted agents callable via API
- **Claude for Microsoft 365** — Office add-in (Excel, Outlook, Teams)

## Architecture (primitives)

The same 4-primitive decomposition Claude Code uses:

| Primitive | Role |
|---|---|
| **Skills** | Domain expertise modules (e.g. SEC filing parsing) |
| **Commands** | Slash-action triggers (`/pitch`, `/reconcile`) |
| **Connectors** | [[Model Context Protocol]] servers — six premium data providers (S&P Global, LSEG, FactSet, Morningstar, Moody's, PitchBook) |
| **Cookbooks** | Deployment templates customers fork & customize |

## Core Agents (Anthropic-shipped)

- **Pitch Agent** — pitchbook drafting
- **Meeting Prep Agent**
- **Market Researcher**
- **Earnings Reviewer** — sell-side analyst workflow
- **Model Builder** — financial-model assembly
- **Valuation Reviewer**
- **GL Reconciler** — controller workflow
- **KYC Screener** — compliance workflow

## Vertical Skill Bundles

Layered above the Core Agents, opinionated configurations:

- **Financial Analysis (Core)** — the base bundle
- **Investment Banking**
- **Equity Research**
- **Private Equity**
- **Wealth Management**
- **Fund Admin & Ops**

## Notable design choices

- **Vertical over horizontal.** Not "use Claude better" — pre-built role-
  specific agents targeting concrete workflows.
- **MCP as the data substrate.** Premium provider connectors mean Claude
  can fetch structured financial data without bespoke integration. This
  is a distribution + moat play.
- **Cookbook-driven customization** — Anthropic ships templates, customers
  modify; not closed boxes.

## When to use it

- Investment banks / hedge funds / RIAs evaluating LLM tooling for
  specific workflows. ✅
- Independent traders or students building from scratch. ❌ — paid product
  + paid data provider stack. See [[TradingAgents Framework]] for the
  open-source alternative (different abstraction layer).

## Distinct from

- **[[TradingAgents Framework]]** — Tauric is an open-source research
  *framework*; Claude for Fin Services is a commercial *product bundle*.
  Different layers, different audiences.

## Open questions

- Are the MCP data-provider connectors official partnerships, or
  third-party wrappers?
- How tightly do the Core Agents coordinate? Is there an orchestration
  layer (think Risk Manager → Trader loop) or are they independent skills?
- Pricing model — Managed Agents API per-call vs per-seat?
