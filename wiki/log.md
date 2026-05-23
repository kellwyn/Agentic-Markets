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
- Domain: trading & markets research. Viewer: Obsidian.
- Created: [[index]], [[log]], [[overview]].
- Empty buckets: `entities/`, `concepts/`, `sources/`, `analyses/`, `journal/`.
- Next: user adds first source to `raw/` and asks for ingest.
