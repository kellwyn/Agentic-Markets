# bryanyzhu/agentic-ai-system-course — README

> **Source kind:** GitHub README (verbatim copy).
> **Source URL:** https://github.com/bryanyzhu/agentic-ai-system-course
> **Fetched:** 2026-05-24
> **About:** A 22-chapter "skeleton" course on designing & operating
> production AI agents. Explicitly inspired by Karpathy's LLM Wiki idea —
> "this course is giving you the skeleton and your agent will help you put
> the muscles on it."

---

## Verbatim README content

# Agentic System Course - Use Agent to Learn Agent

This is a 22-chapter skeleton course on how to design, build, and operate production AI agents — written to be read with your own AI partner at your side. **An agentic system** is an AI system that can autonomously pursue goals by planning, making decisions, using tools, adapting based on feedback, having memory, etc — instead of only responding to a single prompt. A few use cases are:

- **Healthcare**: Multiple AI agents can coordinate patient intake, insurance verification, scheduling, lab monitoring, and discharge planning to automate hospital operations and reduce administrative burden.
- **Customer support**: Specialized AI agents can collaboratively handle ticket triage, knowledge retrieval, sentiment analysis, escalation routing, and follow-up communication to improve support efficiency and response quality.
- **Supply chain**: Multi-agent AI systems can continuously optimize procurement, inventory, production scheduling, and logistics by adapting in real time to disruptions and changing demand.

Similar to [Andrej Karpathy's idea file on LLM-wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f), **this course is giving you the skeleton and your agent will help you put the muscles on it**.

**This course is**:
- A *skeleton* — load-bearing topics, patterns, and decisions, with trade-offs.
- Written to age slowly. Framework specifics rot fast; architectural patterns do not.
- A file pair (course + CLAUDE.md) designed for AI consumption as much as human reading.

**This course is not**:
- A step-by-step tutorial. There is no walked-through project.
- Tied to one stack. The course never says "use LangChain" or "use Pydantic AI." Your AI partner suggests the stack that fits your project.
- A reference manual. When you need an exact API signature, ask your AI or read the docs.

### Course structure

| Chapters | Theme |
|---|---|
| **Ch.00** | How to use this course with your AI partner |
| **Ch.01–04** | Foundations: one tool call → the loop → tools as contract → prompts & cache |
| **Ch.05–08** | Memory and state: short-term → long-term → writing & curation → persistence |
| **Ch.09–11** | Coordination: planning → multi-agent delegation → the harness |
| **Ch.12–14** | External surface: human-in-the-loop → connectors/MCP → skills/MCP/subagents |
| **Ch.15–17** | Production scale: backend → observability → cost, latency, model strategy |
| **Ch.18–19** | Quality and ops: safety/adversarial inputs → operations and forward-deployed |
| **Ch.20–21** | Agency: proactive agents → self-evolving agents |
| **Ch.22** | Design canvas: designing your own agent |

The chapters are ordered so each one only assumes what came before. … *The goal is to ship something you wanted to ship anyway, and to understand every line of it.*

### Optional: reference systems

- **OpenCode** — coding agent (terminal-first, typed tools, sessions, compaction)
- **Hermes Agent** — personal assistant (memory, skills, cron, channels)
- **OpenClaw** — self-hosted personal-assistant gateway (channel adapters)
- **Paperclip** — workflow control plane (multi-agent orchestration, durable Postgres state)

### Repository layout

```
course/         — 22 chapters (read-only by design — this is the skeleton)
CLAUDE.md       — Behavioral guide for your AI partner (read by Claude Code)
AGENTS.md       — Same content as CLAUDE.md, named for Codex / Cursor / other agents
README.md       — This file
setup.sh        — Optional: clone the four reference repos
docs/           — Written notes your AI partner produces on request
questions/      — Daily Q&A log your AI partner writes automatically
workspace/      — Code, exercises, and project builds
references/     — The four reference repos if cloned
```

### One last thing before you start

> "The people shipping the most interesting agentic systems today are not
> the ones with the most experience. **They are the ones who got into a
> tight loop with their AI partner first and stayed in it longest.**"

---

## My read on what's interesting

- **Karpathy-pattern cousin.** This course uses the *same* meta-idea as
  our wiki: a `CLAUDE.md` (here `AGENTS.md` mirror) that an LLM agent
  reads to know how to behave, plus a `course/` skeleton the agent
  fleshes out with the user.
- **22-chapter spine** is the most useful artifact for our purposes —
  it's a categorization of what an "agentic system" actually is.
  Ch.09–11 (coordination / multi-agent / harness) and Ch.12–14
  (MCP / skills / subagents) are directly relevant to anything we
  build on top of the markets domain.
- **Reference repos worth knowing exist** even if we don't clone:
  - OpenCode — coding agent
  - Hermes Agent — personal assistant
  - OpenClaw — self-hosted PA gateway
  - Paperclip — orchestration / workflow plane (Postgres-durable)
- **Explicit anti-framework stance.** "The course never says use
  LangChain or Pydantic AI" — pairs interestingly with
  [[2026-05-24 mindmap tradingagents-framework]] which *does* commit to
  LangGraph + Pydantic. Worth noting that real implementations end up
  framework-coupled even when the design talk pretends otherwise.
- **`docs/`, `questions/`, `workspace/` created on demand** — same
  pattern as our `wiki/analyses/`, `wiki/sources/`, `wiki/journal/`.
  The convergence is not coincidence.
