---
type: source
status: draft
created: 2026-07-11
title: "AI Agent Memory Across Sessions (AI Agents 101, Part 3)"
authors:
- AI Builder Club
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 1.5
url: https://www.aibuilderclub.com/blog/ai-agents-101-part-3
year: 2026
date_published: 2026-04-17
anthropic: false
topic:
- topic/memory
tags:
- memory
- persistence
- course
nlm_id:
nlm_skip: false
watchlist_channel:
af_targets:
- af:ADR-0005
- af:RSCH-04/Q09
- af:RSCH-04/Q11
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 6776c49b3be5f762225b730d0eeff6f0c5136bff2afa3596905630062754326d
---

# AI Agent Memory Across Sessions (AI Agents 101, Part 3)

> AI Builder Club, "AI Agent Memory Across Sessions (AI Agents 101, Part 3)", Build AI Agents Course, 17 April 2026 (updated 11 June 2026), https://www.aibuilderclub.com/blog/ai-agents-101-part-3.

## Summary

Every LLM API call is stateless; a model has no built-in session memory, so persistence is entirely the developer's responsibility. The lesson lays out three memory patterns of increasing durability — in-context, external file, and vector database — and a decision rule for choosing among them: start with in-context, move to an external file once persistence matters, and add a vector database only once the file gets unwieldy.

## Key Concepts

- LLM statelessness is a design choice for predictability, safety, and scalability, not a temporary limitation.
- In-context memory is bounded by the context window and disappears entirely when the session ends.
- External file memory (Markdown for prose, JSON for structured facts) persists across sessions but degrades once facts reach the hundreds or thousands.
- Vector database memory retrieves by semantic similarity and scales past the point external files break down.
- The 2026 "memory layer" (Mem0) sits above a vector database and adds extraction, deduplication, conflict resolution, and user-scoped retrieval that a raw vector store does not provide.

## Terminology

- Stateless API — every call operates independently; no session history is retained by the model.
- In-context memory — memory that exists only as the current message list within one session.
- Embedding — a numerical representation of semantic meaning used for similarity search.
- Memory layer — an abstraction, such as Mem0, that manages fact extraction, deduplication, and user scoping on top of a vector store.

## Architecture and Implementation

The external-file pattern reads a Markdown or JSON file at session start and injects it into the system prompt; the agent signals new facts with a `MEMORY UPDATE:` marker that wrapper code parses and appends to disk. The vector-database pattern hashes facts into IDs, stores them with timestamps in a store such as ChromaDB, and retrieves the top-N semantically similar facts per query rather than the entire store; a `REMEMBER:` marker in agent output triggers a new write. The 2026 landscape adds Mem0 as an extraction-reconciliation layer above the vector store, and `agentmemory` for Claude Code implements four-tier consolidation (working, short-term, long-term, archival).

## Code Examples

The lesson provides `load_memory()` / `save_memory()` functions for the Markdown pattern, an `add_decision()` helper for the structured-JSON pattern, and `add_memory()` / `query_memory()` functions for the ChromaDB pattern, each wired into a modified agent loop that parses the relevant marker syntax from model output.

## Best Practices

- Persist only decisions, preferences, and architectural choices — not routine interactions.
- Version memory files with simple timestamped backups.
- Add timestamps to every memory entry to support staleness detection.
- Progress from in-context, to external file, to vector database only as each prior tier breaks down in practice.

## Warnings and Anti-Patterns

- Over-storing every interaction defeats the purpose of memory as signal.
- Skipping version control on memory files loses the ability to recover from a bad write.
- Reaching for a vector database before an external file has actually failed is premature optimisation.
- Unflagged stale facts silently contaminate later decisions.

## Related Concepts

- [[memory]]
- [[the-agent-loop]]
- [[claude-code]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The series continues into multi-agent orchestration (Part 4) and production deployment (Part 5); the deeper memory-taxonomy treatment (episodic, semantic, procedural) is covered separately in [[10_Sources/Blog/agent-memory-systems-guide|Agent Memory Systems: The Complete Guide]].

## References

- AI Agent Memory Across Sessions (AI Agents 101, Part 3) — https://www.aibuilderclub.com/blog/ai-agents-101-part-3
