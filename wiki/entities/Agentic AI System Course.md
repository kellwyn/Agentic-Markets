---
type: entity
created: 2026-05-24
updated: 2026-05-24
tags: [course, skeleton, karpathy-pattern, framework-agnostic, education]
sources: ["[[2026-05-24 bryanyzhu-agentic-ai-course]]"]
confidence: medium
---

# Agentic AI System Course (bryanyzhu)

> A 22-chapter "skeleton" course on designing, building, and operating
> production AI agents. Read with your own AI partner; the course supplies
> the spine and the agent supplies the muscles.

**Repo:** https://github.com/bryanyzhu/agentic-ai-system-course
**Author:** bryanyzhu

## What it is

A repository of 22 chapter markdown files plus a `CLAUDE.md` /
`AGENTS.md` behavioral guide. Not a tutorial; not a reference manual.
The course pages are deliberately load-bearing patterns + trade-offs, and
the AI agent (Claude Code / Codex / Cursor) supplies the framework-
specific implementation when you ask.

Directly inspired by [[Karpathy LLM Wiki]] — both are instances of the
*skeleton + AI muscles* meta-pattern.

## Course spine (8 thematic blocks)

| Block | Chapters | Theme |
|---|---|---|
| Foundations | Ch.01–04 | one tool call → loop → tools as contract → prompts & cache |
| Memory & state | Ch.05–08 | short-term → long-term → curation → persistence |
| Coordination | Ch.09–11 | planning → multi-agent delegation → harness |
| External surface | Ch.12–14 | HITL → connectors/MCP → skills/subagents |
| Production scale | Ch.15–17 | backend → observability → cost/latency/model |
| Quality & ops | Ch.18–19 | safety/adversarial → operations |
| Agency | Ch.20–21 | proactive → self-evolving |
| Capstone | Ch.22 | design canvas |

## Notable design choices

- **Framework-agnostic by policy.** Refuses to name LangChain, LangGraph,
  Pydantic AI, etc. Defers stack choice to "your AI partner." Sits in
  productive tension with implementations like
  [[TradingAgents Framework]] that hard-commit to LangGraph.
- **Pair-file convention.** `CLAUDE.md` and `AGENTS.md` are content-
  identical because different agents look for different filenames by
  default. Worth mirroring in this wiki if/when a Codex-family agent
  is added.
- **On-demand directories.** `docs/`, `questions/`, `workspace/` are
  created as the agent works. Same shape as this wiki's `analyses/`,
  `journal/`, etc.
- **No walked-through project.** Resists tutorial-style hand-holding;
  forces the reader to instantiate against their own project.

## Reference systems (clonable via `setup.sh`)

Four open-source examples the course occasionally points at:

- **OpenCode** — coding agent (terminal-first, typed tools, sessions,
  compaction)
- **Hermes Agent** — personal assistant (memory, skills, cron, channels)
- **OpenClaw** — self-hosted PA gateway (channel adapters)
- **Paperclip** — workflow control plane (orchestration, durable
  Postgres state)

Not yet ingested as separate entities — file them only if you actually
clone and read code.

## When to engage

- Designing or building an agentic system from scratch — use as the
  spine to your AI partner's coding work. ✅
- As a reference for "what should I be thinking about?" when planning an
  agent project. ✅
- As a how-to for a specific framework. ❌ — by design, not its job.

## Notable connections

- [[Karpathy LLM Wiki]] (referenced in the README, not yet a wiki entity
  — currently captured in this wiki's CLAUDE.md schema).
- [[Model Context Protocol]] (Ch.12–14).
- Conceptually informs [[Multi-Agent LLM Trading Systems]] (Ch.09–11
  coordination block).

## Open questions

- Individual chapter content is not yet read. Worth ingesting Ch.10
  (multi-agent delegation) or Ch.16 (observability) as separate sources
  when relevant to a specific build.
- Update cadence — is the course actively maintained?
