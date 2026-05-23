---
type: source
created: 2026-05-24
updated: 2026-05-24
source_kind: article
source_url: https://github.com/bryanyzhu/agentic-ai-system-course
source_path: raw/articles/2026-05-24 bryanyzhu-agentic-ai-system-course.md
tags: [area/agents, course, skeleton, karpathy-pattern, framework-agnostic]
---

# bryanyzhu/agentic-ai-system-course (GitHub)

**Source:** https://github.com/bryanyzhu/agentic-ai-system-course — raw
README captured to
[[2026-05-24 bryanyzhu-agentic-ai-system-course|raw/articles/]].
**Fetched:** 2026-05-24.
**Author:** bryanyzhu.

## TL;DR
- A **22-chapter "skeleton" course** on designing and operating
  production AI agents, explicitly written to be read alongside an AI
  partner that fills in the details.
- Self-described cousin of [[Karpathy LLM Wiki]] — the pattern of *human
  curates skeleton + LLM provides muscles* applied to teaching instead
  of knowledge accumulation.
- **Explicitly framework-agnostic.** Refuses to commit to LangChain,
  Pydantic AI, LangGraph, etc. Defers stack choice to "your AI partner."
- Course spine: Foundations → Memory & State → Coordination →
  External Surface (HITL, MCP, subagents) → Production Scale → Quality
  & Ops → Agency (proactive, self-evolving) → Design Canvas.
- Optional reference systems (clonable via `setup.sh`): **OpenCode**
  (coding agent), **Hermes Agent** (personal assistant), **OpenClaw**
  (PA gateway), **Paperclip** (orchestration / Postgres-durable state).

## Key takeaways
- **The Karpathy meta-pattern keeps appearing.** Karpathy's LLM Wiki
  gist (skeleton + AI fills the muscles) directly inspired this course,
  which in turn inspires this wiki. The pattern *generalizes*: it works
  for personal knowledge bases, for courses, and probably for product
  specs and project plans.
- **`CLAUDE.md` + `AGENTS.md` duplicate-named for agent compatibility.**
  Same content, two filenames, because Claude Code reads CLAUDE.md and
  Codex/Cursor read AGENTS.md by default. Worth mirroring in this repo
  if you ever switch to a Codex-family agent.
- **`docs/`, `questions/`, `workspace/` created on demand** — Bryan's
  course converges on the same directory taxonomy as our `wiki/analyses`,
  `wiki/sources`, `wiki/journal`. Multiple independent attempts arrive
  at similar shapes.
- **Anti-framework stance in tension with implementations.** This course
  refuses to name a stack. The [[TradingAgents Framework]] commits
  hard to LangGraph + Pydantic. Both can be right: the *teaching* is
  framework-agnostic, but every *implementation* ends up framework-
  coupled. The wiki should preserve this tension.

## Notable quotes (verbatim)
> "An agentic system is an AI system that can autonomously pursue goals
> by planning, making decisions, using tools, adapting based on feedback,
> having memory, etc — instead of only responding to a single prompt."

> "The people shipping the most interesting agentic systems today are
> not the ones with the most experience. They are the ones who got into
> a tight loop with their AI partner first and stayed in it longest."

## Chapter structure (one-line each)
| Block | Chapters | Theme |
|---|---|---|
| Foundations | Ch.01–04 | one tool call → the loop → tools as contract → prompts & cache |
| Memory & state | Ch.05–08 | short-term → long-term → writing & curation → persistence |
| Coordination | Ch.09–11 | planning → multi-agent delegation → the harness |
| External surface | Ch.12–14 | HITL → connectors/MCP → skills/MCP/subagents |
| Production scale | Ch.15–17 | backend → observability → cost/latency/model strategy |
| Quality & ops | Ch.18–19 | safety/adversarial → operations & forward-deployed |
| Agency | Ch.20–21 | proactive → self-evolving |
| Capstone | Ch.22 | design canvas |

## Open questions
- The chapters themselves are not yet read — only the README. Worth
  ingesting individual chapters as separate sources when relevant to a
  build (e.g. Ch.10 "multi-agent delegation" for the trading-agents
  discussion).
- Reference systems (OpenCode, Hermes, OpenClaw, Paperclip) are not yet
  in the wiki. They're worth their own entity pages *if* you actually
  clone and read them — until then they're stub-bait.

## Notable connections
- This source is the strongest argument for [[Karpathy LLM Wiki]] as a
  meta-pattern entry, but we haven't filed Karpathy's gist as its own
  source yet. (It's referenced in this wiki's CLAUDE.md schema — the
  schema is effectively the meta-source. Worth filing properly later.)
- Ch.09–11 (Coordination) is the chapter block directly relevant to
  [[Multi-Agent LLM Trading Systems]] and [[Agent Role Specialization]].
- Ch.12 (Connectors/MCP) connects to [[Model Context Protocol]] and
  [[Claude for Financial Services]].

## Wiki updates made (this ingest)
- Created [[Agentic AI System Course]] entity
- Strengthened [[Multi-Agent LLM Trading Systems]] with the framework-
  agnostic counterpoint
- Strengthened [[Model Context Protocol]] (Ch.12–14 connection)
- Updated [[overview]] to call out the recurring skeleton+AI meta-pattern
