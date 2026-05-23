# Agentic-Markets

A personal **LLM Wiki** on **agentic AI systems applied to markets and
trading**, set up following
[Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

- **Maintainer:** Claude (via Claude Code) — reads sources, writes pages, keeps cross-references current.
- **You:** curate the source pile in `raw/`, ask questions, review changes in Obsidian, push to GitHub.
- **Viewer:** [Obsidian](https://obsidian.md/) — open this repo as a vault.

## What's in scope

Two interlocking areas:

1. **Markets / trading research** — regimes, strategies, instruments, indicators, risk, backtesting.
2. **Agentic AI systems for finance** — multi-agent LLM architectures, frameworks (LangGraph, MCP, TradingAgents), orchestration patterns, memory, tool design, evaluation.

Bridge pages — anything that connects the two (e.g. *how a multi-agent system reasons about market regimes*) — are the most valuable.

## TL;DR layout

```
raw/    ← drop sources here (papers, articles, repos, notes, data). Immutable.
wiki/   ← Claude builds & maintains this. Open in Obsidian.
CLAUDE.md ← the schema. Claude reads this every session to know how to behave.
```

## How a session goes

1. **Add a source** to `raw/` (a paper, web clipping, GitHub README, screenshot of a mind map).
2. **Open Claude Code** in this directory and say _"ingest raw/papers/2026-05-24-foo.pdf"_.
3. **Discuss** — Claude surfaces takeaways before writing.
4. **Approve** the writes — Claude updates 1–15 wiki pages, the index, and the log.
5. **Browse** in Obsidian — the graph view shows new connections.
6. **Commit & push** — `git add . && git commit && git push`.

For questions, just ask. Claude reads `wiki/index.md` first, drills into relevant pages, answers with `[[wikilinks]]`, and may file the answer back as a new analysis page.

For periodic health-checks: ask Claude to **lint** the wiki — it will report contradictions, stale claims, orphan pages, and missing concepts.

## First-time setup

1. Open this folder in Obsidian (File → Open Vault → choose this directory).
2. Recommended Obsidian plugins:
   - **Dataview** — query the YAML frontmatter on wiki pages
   - **Marp slides** — generate slide decks from markdown
   - **Obsidian Web Clipper** — browser extension for ingesting articles
3. In Obsidian settings → Files & Links: set "Attachment folder path" to
   `raw/assets`. In Hotkeys: bind "Download attachments for current file"
   to `Ctrl+Shift+D`.

## OneDrive note

This vault lives in OneDrive, which syncs automatically. Convenient for
backup but watch for `*.conflict.*` files if you edit on two machines at
once. The `.gitignore` filters those.

## See also

- [CLAUDE.md](CLAUDE.md) — full schema (read before customizing conventions)
- [wiki/index.md](wiki/index.md) — catalog of every wiki page
- [wiki/log.md](wiki/log.md) — chronological record of every ingest / query / lint
- [wiki/overview.md](wiki/overview.md) — living synthesis of what the wiki currently believes
