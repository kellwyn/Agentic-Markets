# Log

Append-only chronological record. Newest entries at the bottom. Every entry
starts with `## [YYYY-MM-DD] <op> | <short title>` so the file stays
grep-parseable.

Ops: `ingest` · `query` · `analysis` · `lint` · `meta`.

Quick recent-history check:
- bash: `grep "^## \[" log.md | tail -10`
- PowerShell: `Select-String "^## \[" log.md | Select-Object -Last 10`

---

## [2026-05-24] meta | wiki initialized
- Bootstrapped directory layout and [[CLAUDE]] schema following the
  [Karpathy LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).
- Domain: agentic AI for markets & trading. Viewer: Obsidian.
- Created: [[index]], [[log]], [[overview]].
- Empty buckets: `entities/`, `concepts/`, `sources/`, `analyses/`, `journal/`.
- Initially scaffolded at `C:\Users\kellw\OneDrive\LLMWiki-Claude\` then
  migrated to GitHub-tracked repo `kellwyn/Agentic-Markets`.

## [2026-05-24] ingest | first batch — 5 agentic-AI + markets sources
Batched ingest (user-approved exception to the one-at-a-time default).

### Sources filed
- [[2026-05-24 claude-for-financial-services]] — Anthropic vertical product mindmap
- [[2026-05-24 market-regimes-framework]] — three-pillar regime framework mindmap (India-flavored)
- [[2026-05-24 tradingagents-framework-mindmap]] — TradingAgents impl view
- [[2026-05-24 tauric-tradingagents-paper]] — arXiv 2412.20138v7 (Tauric Research)
- [[2026-05-24 bryanyzhu-agentic-ai-course]] — 22-chapter skeleton course

### New entities (6)
- [[TradingAgents Framework]]
- [[Tauric Research]]
- [[Claude for Financial Services]]
- [[LangGraph]]
- [[Model Context Protocol]]
- [[Agentic AI System Course]]

### New concepts (6)
- [[Multi-Agent LLM Trading Systems]] (umbrella)
- [[Agent Role Specialization]]
- [[Bull-Bear Debate]]
- [[Structured Agent Communication]]
- [[Market Regimes]]
- [[Backtest Validity]]

### Tensions surfaced
- **Framework commitment vs agnosticism**: TradingAgents commits to
  LangGraph + Pydantic; Agentic AI System Course refuses to name a stack.
  Captured on [[LangGraph]] and [[Agentic AI System Course]].
- **Tauric paper SR=8.21 vs authors' own caveat** — preserved verbatim
  on [[2026-05-24 tauric-tradingagents-paper]] and turned into the
  [[Backtest Validity]] concept page.
- **Two TradingAgents views diverge on role list** — paper has 7 roles
  ending in Fund Manager; mindmap adds Research Manager + Portfolio
  Manager. Flagged on [[TradingAgents Framework]]; verify upstream.

### Open threads added to [[overview]]
- Verify TradingAgents role list against upstream.
- Bridge [[Market Regimes]] into [[Multi-Agent LLM Trading Systems]].
- Cost-of-evidence: cheapest valid multi-regime backtest?
