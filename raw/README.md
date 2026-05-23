# raw/ — immutable source documents

This is the **source of truth**. Claude reads from here; Claude never writes
or modifies anything in this folder. If a source is wrong or needs context,
note it on the corresponding wiki source page in `wiki/sources/`, don't edit
the original.

## What goes where

| Folder      | What goes in it                                              |
|-------------|--------------------------------------------------------------|
| `articles/` | Web articles, blog posts. Obsidian Web Clipper output lands here. |
| `papers/`   | Academic / research PDFs and arXiv preprints.                |
| `notes/`    | Your raw notes — journal dumps, podcast transcripts, screenshots of charts, scratch thinking. |
| `assets/`   | Images downloaded by Obsidian's "Download attachments for current file" command. |
| `data/`     | CSVs, tick data samples, backtest exports, IS/OOS splits.    |

You can add new top-level buckets if a kind of source doesn't fit (e.g.
`videos/`, `books/`). Just mention it next session so Claude can update
[CLAUDE.md](../CLAUDE.md).

## Ingest workflow (for you, the human)

1. Drop the source into the right `raw/` subfolder.
2. Open the Claude Code session and say something like
   _"ingest raw/articles/2026-05-24-foo.md"_.
3. Discuss takeaways. Approve emphasis.
4. Claude writes the source summary, updates affected wiki pages, logs it.
5. Browse the diff in Obsidian's graph view.

## Obsidian Web Clipper tip

In Obsidian settings:
- **Files and links → Attachment folder path**: set to `raw/assets`.
- **Hotkeys → "Download attachments for current file"**: bind to e.g.
  `Ctrl+Shift+D`.

After clipping a web article, hit the hotkey and all images get pulled local
into `raw/assets/`. This means Claude can reference them later instead of
chasing dead URLs.
