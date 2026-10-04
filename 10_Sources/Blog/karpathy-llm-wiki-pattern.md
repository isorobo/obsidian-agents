---
type: source
status: draft
created: 2026-07-11
title: "Karpathy's LLM Wiki: A Knowledge Base That Compounds"
authors:
- AI Builder Club
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 1.12 (commentary on Andrej Karpathy's April 2026 GitHub Gist)
url: https://www.aibuilderclub.com/blog/karpathy-llm-wiki
year: 2026
date_published: 2026-05-27
anthropic: false
topic:
- topic/memory
- topic/karpathy
tags:
- karpathy
- llm-wiki
- obsidian
- course
nlm_id:
nlm_skip: false
watchlist_channel:
af_targets:
- af:ADR-0005
- af:RSCH-04/Q11
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: f3ccaea3c61990e527653b090bb9a1b9ec0dac21905275cd61e68519dbc3fc80
---

# Karpathy's LLM Wiki: A Knowledge Base That Compounds

> AI Builder Club, "Karpathy's LLM Wiki: A Knowledge Base That Compounds", Build AI Agents Course, 27 May 2026 (updated 29 June 2026), https://www.aibuilderclub.com/blog/karpathy-llm-wiki. AI Builder Club's commentary on Andrej Karpathy's April 2026 GitHub Gist, not Karpathy's original document.

## Summary

Standard RAG retrieves chunks at query time and accumulates nothing across sessions; every query re-finds and re-assembles fragments from scratch. Karpathy's pattern instead has the model maintain a persistent, compounding Markdown wiki — his framing: "Obsidian is the IDE. The LLM is the programmer. The wiki is the codebase." A three-layer architecture (raw sources, an LLM-owned wiki, and a schema file) and three operations (ingest, query, lint) give the model, not the human, ownership of the bookkeeping that causes human-maintained wikis to collapse under their own maintenance burden. This is the pattern this vault, `wiki-agents`, itself implements.

## Key Concepts

- RAG synthesises knowledge repeatedly per query; the LLM wiki synthesises once and accumulates, producing pages that compound rather than fragments that get re-derived.
- Three layers separate concerns: raw sources are immutable and read-only, the wiki is entirely LLM-owned and LLM-written, and a schema file (`CLAUDE.md` or `AGENTS.md`) defines structure, conventions, and ingestion workflow.
- Three operations run the system: ingest (), query (search, synthesise, cite, and file good answers back as new pages), and lint (a periodic pass finding contradictions, stale claims, orphan pages, and missing cross-references).
- The bottleneck in human-maintained wikis is not thinking or reading, it is bookkeeping — and that is precisely the part an LLM does not get bored of.
- The `index.md` catalogue and `log.md` append-only chronological record are named as the two files that keep an LLM oriented as the wiki scales, sufficient without vector search up to a few hundred pages.

## Terminology

- LLM wiki — a persistent, LLM-maintained Markdown knowledge base that compounds across ingestion sessions rather than resetting per query.
- Ingest — the operation where the model reads new source material, writes a summary, and updates the index plus roughly ten to fifteen relevant wiki pages.
- Lint — a periodic health-check operation where the model finds contradictions, stale claims, orphan pages, and missing cross-references, and proposes new research questions.
- Three-layer architecture — raw sources (immutable), the wiki (LLM-owned), and the schema (the configuration file defining how the first two relate).

## Architecture and Implementation

Layer 1 holds curated, immutable raw sources that the model reads but never edits. Layer 2 is the wiki itself — summaries, entity pages, concept pages, comparisons, and synthesis — owned entirely by the model. Layer 3 is a schema configuration file that turns a generic chatbot into a disciplined wiki maintainer by defining structure and ingestion rules. `index.md` acts as a content-oriented catalogue the model reads first when answering a query, listing links, one-line summaries, and metadata by category; `log.md` is an append-only chronological record of every ingest, query, and lint pass, in a consistent parseable prefix format such as `## [2026-04-02] ingest | Article Title`.

## Code Examples

None as runnable code; the lesson instead gives a getting-started sequence: create a `raw/` folder for sources and a `wiki/` folder for LLM output, write a `CLAUDE.md` schema describing structure and workflow, clip five to ten articles with the Obsidian Web Clipper, ingest them one at a time while staying engaged with the output, then query the built wiki and file good answers back as new pages.

## Best Practices

- Start small; the wiki compounds value from the first source ingested, not after a large upfront population effort.
- Keep raw sources immutable and separate from the LLM-owned wiki layer; do not let the model edit its own evidence.
- Use `index.md` as the first-read catalogue and `log.md` as the append-only audit trail so the model stays oriented as the corpus grows.
- Reach for a local BM25 or vector re-ranking tool such as [[10_Sources/Repos/qmd-local-hybrid-search|qmd]] only once the wiki passes a few hundred pages — not before.
- Keep the human role to curation, direction, and meaning; keep the LLM role to bookkeeping and consistency.

## Warnings and Anti-Patterns

- Traditional second-brain tools (Obsidian, Notion, Roam) depend on human filing and collapse when human maintenance falls behind; the LLM wiki removes that single point of failure by design.
- Treating the wiki purely as chunked RAG storage forfeits the compounding benefit the pattern is built for.
- Skipping the lint operation lets contradictions, stale claims, and orphan pages accumulate silently.

## Related Concepts

- [[memory]]
- [[what-is-an-ai-agent]]
- [[20_People/andrej-karpathy/profile|Andrej Karpathy]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson traces the idea back to Vannevar Bush's 1945 Memex — a personal, curated knowledge system with associative trails — and frames the LLM wiki as the first practical solution to the maintenance problem Bush could not solve. A future research pass should source Karpathy's original April 2026 GitHub Gist directly rather than this secondary summary.

## References

- Karpathy's LLM Wiki: A Knowledge Base That Compounds — https://www.aibuilderclub.com/blog/karpathy-llm-wiki
