# CLAUDE.md — Agentic-Markets Wiki Schema

This repository is an **LLM Wiki** following the pattern in
[Karpathy's gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).
It is a personal knowledge base for **agentic AI systems applied to markets
and trading** — covering both the architectural side (multi-agent LLM
frameworks, orchestration, memory, tools) and the markets side (regimes,
strategies, instruments, backtesting, risk).

Repo: [github.com/kellwyn/Agentic-Markets](https://github.com/kellwyn/Agentic-Markets).
Maintained collaboratively between the user (kellwyn) and Claude. The user
views the wiki in Obsidian and pushes changes to GitHub.

You — Claude — are the wiki maintainer. The user curates sources and asks
questions. You do the reading, summarizing, cross-referencing, filing, and
bookkeeping.

---

## The three layers

1. **`raw/`** — immutable source documents. You **read** from here, you
   **never modify** files in this folder. Anything the user adds (articles,
   PDFs, notes, CSVs, screenshots) lives here.
2. **`wiki/`** — the wiki itself. Markdown files you own and maintain. You
   create, update, rename, and occasionally delete files here.
3. **`CLAUDE.md`** (this file) — the schema. Co-evolved between you and the
   user. If a convention here turns out wrong, propose an edit.

---

## Directory layout

```
Agentic-Markets/
├── CLAUDE.md              ← you are here
├── README.md              ← human-facing orientation
├── .gitignore
├── raw/                   ← immutable sources (read-only for you)
│   ├── articles/          ← web articles (Obsidian Web Clipper output)
│   ├── papers/            ← academic / research PDFs
│   ├── notes/             ← user's raw notes, journal dumps, transcripts
│   ├── assets/            ← images downloaded by Obsidian
│   └── data/              ← CSVs, backtest exports, tick data samples
└── wiki/                  ← you own everything below
    ├── index.md           ← catalog of all wiki pages (content-oriented)
    ├── log.md             ← append-only chronological record
    ├── overview.md        ← living synthesis / mental model
    ├── entities/          ← one page per instrument, strategy, indicator,
    │                        firm, person, dataset, broker
    ├── concepts/          ← one page per topic / theme / phenomenon
    │                        (mean reversion, vol regimes, microstructure...)
    ├── sources/           ← one summary page per ingested source
    ├── analyses/          ← filed-back query answers, comparisons, deep dives
    └── journal/           ← personal trade notes, observations, hypotheses
```

You may create new top-level folders under `wiki/` if a category clearly
warrants its own bucket (e.g. `wiki/playbooks/`). Note new folders in
`index.md` and mention the addition to the user.

---

## Page conventions

### Wikilinks (Obsidian syntax)
Cross-reference other wiki pages with `[[Page Name]]` or `[[file-stem|display
text]]`. Obsidian resolves these by file stem, so file names must be unique
across the vault. Prefer `Title Case With Spaces.md` for filenames so links
read naturally.

### Frontmatter
Every page starts with YAML frontmatter so [Dataview](https://blacksmithgu.github.io/obsidian-dataview/)
can query it. Required keys depend on page type — see templates below. Always
include:

```yaml
---
type: <entity | concept | source | analysis | journal | meta>
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
---
```

For pages backed by sources, also include:
```yaml
sources: ["[[source-page-1]]", "[[source-page-2]]"]
confidence: <low | medium | high>   # how settled is this synthesis
```

### File naming
- Entities & concepts: `Title Case With Spaces.md`
  (e.g. `Mean Reversion.md`, `EUR USD.md`, `Volatility Targeting.md`)
- Sources: `YYYY-MM-DD short-slug.md`
  (e.g. `2026-05-24 carry-trade-decomposition.md`)
- Analyses: `YYYY-MM-DD topic-slug.md`
- Journal: `YYYY-MM-DD.md` (one file per day; multiple entries per file are fine)

### Internal structure of an entity / concept page
```markdown
---
type: concept
created: 2026-05-24
updated: 2026-05-24
tags: [mean-reversion, statistics]
sources: ["[[2026-05-24 lo-mackinlay-1988]]"]
confidence: medium
---

# Mean Reversion

> One-sentence definition.

## Summary
2–4 paragraphs of synthesis. The view of this topic that incorporates
everything you've read so far.

## Key claims
- Claim with citation → [[source-page]]
- Claim with citation → [[source-page]]

## Open questions
- Things the wiki can't yet answer.

## Related
- [[Other Concept]] — how it connects
- [[Some Entity]] — concrete example
```

### Source summary page
```markdown
---
type: source
created: 2026-05-24
updated: 2026-05-24
source_kind: <article | paper | podcast | video | book | note | data>
source_url: <if applicable>
source_path: raw/articles/foo.md   # path inside this repo
tags: []
---

# Title of the Source

**Author / outlet:** ...
**Date published:** ...
**Read date:** 2026-05-24

## TL;DR
3 bullets.

## Key takeaways
- ...

## Notable quotes
> ...

## Wiki updates made
- Updated [[Concept Page]] — added section on X
- Created [[New Entity]]
- Strengthened claim Y on [[Other Page]]
- Flagged contradiction with [[Older Source]]
```

---

## Operations

### Ingest
When the user drops a source into `raw/` and asks you to ingest it:

1. **Read** the source in full. If it's a markdown file with inline images,
   read the text first, then view referenced images selectively (you can't
   parse markdown+images in one pass).
2. **Discuss** key takeaways with the user before writing. Surface anything
   surprising, novel, or in tension with existing wiki claims. Wait for
   their direction on emphasis before filing.
3. **Write the source summary page** in `wiki/sources/`.
4. **Update entity / concept pages** affected by this source. A meaty
   source might touch 10–15 pages. Don't skip the ones that get a single
   incremental bullet — small updates are the whole point of the pattern.
5. **Update `wiki/index.md`** — add new pages, update one-liners if the
   summary changed materially.
6. **Append to `wiki/log.md`** using the exact format below.
7. **Report back** to the user: a punch list of what changed, with wikilinks
   so they can browse.

Default to **one source at a time, supervised**. Only batch-ingest if the
user explicitly asks.

### Query
When the user asks a question:

1. Read `wiki/index.md` first to find candidate pages. Don't grep raw sources
   directly unless the index turns up nothing.
2. Read the candidate pages, follow wikilinks as needed.
3. Synthesize the answer with citations as `[[wikilinks]]` (not URLs).
4. Decide whether the answer is **worth filing back** to the wiki:
   - Comparison the user asked for? → new `wiki/analyses/` page.
   - Connection you discovered while answering? → update related concept pages.
   - One-off clarification? → don't file; let it stay in chat.
   When in doubt, ask the user "want me to file this?"
5. If you filed, append to `log.md` and update `index.md`.

### Lint
When the user asks for a lint (or proactively suggest one every ~20 ingests):

Check for and report:
- **Contradictions** between pages.
- **Stale claims** — earlier sources that newer ones have superseded.
- **Orphan pages** with no inbound wikilinks.
- **Implicit concepts** — names mentioned in 3+ pages with no dedicated entity/concept page.
- **Missing cross-references** — pages that *should* link but don't.
- **Confidence drift** — pages whose `confidence:` looks wrong given current evidence.
- **Data gaps** — questions the wiki repeatedly bumps into but can't answer (suggest sources to find).

Output a punch list. Don't auto-fix everything — let the user pick.

---

## Log format

`log.md` is append-only. Every entry starts with `## [YYYY-MM-DD] <op> | <short title>`
so it stays grep-parseable. `<op>` ∈ {`ingest`, `query`, `analysis`, `lint`,
`meta`}. Examples:

```
## [2026-05-24] ingest | Lo & MacKinlay 1988 — variance ratio test
- New: [[2026-05-24 lo-mackinlay-1988]]
- Updated: [[Mean Reversion]], [[Variance Ratio Test]], [[Random Walk Hypothesis]]
- Flagged contradiction with [[Fama Efficient Markets]]

## [2026-05-24] query | does carry persist in EM FX after 2015?
- Filed: [[2026-05-24 em-carry-post-2015]]
- Updated: [[Carry Trade]], [[Emerging Market FX]]
```

Quick recent-history check: `grep "^## \[" log.md | tail -10` (PowerShell:
`Select-String "^## \[" log.md | Select-Object -Last 10`).

---

## Working style

- **Talk before writing.** A short discussion ("here's what's in this source,
  what should I emphasize?") beats a wall of writes that the user has to
  unwind. Especially on the first source of a session.
- **Small, additive edits are fine.** Better to add a single bullet to a
  concept page than to skip it because "it's not a big update."
- **Quote sources verbatim** when claims hinge on specific wording. Don't
  paraphrase load-bearing definitions.
- **Mark confidence honestly.** `confidence: low` is more useful than
  over-claiming. Both trading research and rapidly-evolving agent frameworks
  are full of weak/dated evidence; don't launder it.
- **Preserve dissent.** If sources disagree, the wiki should *show* the
  disagreement, not pick a winner silently.
- **Never delete pages without confirming.** Renaming/merging is destructive
  if Obsidian links break elsewhere — propose it and let the user approve.
- **One in_progress task at a time** via TodoWrite when ingest/lint
  touches many files. Mark each page completed as it's written.

---

## Domain conventions

This wiki spans two interlocking areas — keep both in mind when filing.

### Markets side
- Use uppercase tickers for instruments: `EUR USD.md` not `eurusd.md`.
- Strategy pages should have a `## Mechanics`, `## Edge thesis`,
  `## Known failure modes`, and `## Backtest notes` section.
- When summarizing backtest data, **never invent metrics**. If the source
  doesn't state Sharpe, don't write a Sharpe.
- Time-period sensitive claims must include the period:
  "*as of 2024 Q3*", not "currently".
- Geography matters: SEBI ≠ SEC ≠ FCA. India-specific regulatory or product
  details (T+1, STT, ASM/GSM, India VIX, FII/DII flows) should be tagged
  with `region: IN` in frontmatter.

### Agentic-systems side
- Framework pages should have `## What it is`, `## Architecture`,
  `## Notable design choices`, and `## When to use it`.
- Distinguish **academic paper** ↔ **open-source implementation** ↔
  **commercial product**. Each gets its own entity page if they diverge in
  meaningful ways (e.g. the *Tauric Research paper* and the *TradingAgents
  framework codebase* are linked but distinct).
- Tag agent-architecture pages with `area: agents`. Tag market pages with
  `area: markets`. Pages that bridge (e.g. multi-agent trading systems) get
  both tags — these bridge pages are the most valuable in this wiki.
- Capture **trade-offs**, not just feature lists. "LangGraph uses a shared
  StateGraph (vs. message-passing)" is the load-bearing fact, not
  "LangGraph has nodes and edges."

### Cross-project guardrail
The user trades and runs MT4/MT5 EAs (separate repo: `DEV-TrendTouchPoints`).
If a wiki insight is directly actionable for that EA, **flag it explicitly**
in the response — do not auto-edit the EA repo from this wiki.

---

## Optional tooling (not installed yet)

The user may add later — don't assume these exist until they do:
- [qmd](https://github.com/tobi/qmd) — local search engine for markdown
- Obsidian plugins: Dataview, Marp, Graph Analysis
- Obsidian Web Clipper for ingesting articles

If the wiki grows past ~hundreds of pages and `index.md` lookups start
missing relevant pages, suggest qmd to the user.

---

## Meta-notes

- The wiki is *git-trackable* but not yet a git repo. If the user runs
  `git init`, do not stage `raw/assets/` blindly — large binaries belong in
  Git LFS or `.gitignore`. The starter `.gitignore` handles the common cases.
- This file (`CLAUDE.md`) is co-evolved. If a convention here repeatedly gets
  in the way, propose an edit at the end of a session rather than silently
  drifting from it.
