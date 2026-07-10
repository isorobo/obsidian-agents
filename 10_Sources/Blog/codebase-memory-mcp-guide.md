---
type: source
status: draft
created: 2026-07-11
title: "Codebase Memory MCP: Give Your Coding Agent a Map (2026)"
authors:
- Jason Zhou
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 3.13
url: https://www.aibuilderclub.com/blog/codebase-memory-mcp-guide
year: 2026
date_published: 2026-07-05
anthropic: false
topic:
- topic/mcp
tags:
- codebase-memory
- knowledge-graph
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
---

# Codebase Memory MCP: Give Your Coding Agent a Map (2026)

> Jason Zhou, "Codebase Memory MCP: Give Your Coding Agent a Map (2026)", AI Builder Club, Build AI Agents Course, 5 July 2026, https://www.aibuilderclub.com/blog/codebase-memory-mcp-guide.

## Summary

Chapter 3 closes where it started, with the cost of forcing a model to read raw source instead of structured meaning: a typical grep-then-read-then-reconstruct exploration loop burns roughly a hundred input tokens per output token. Codebase Memory MCP is an MIT-licensed server that indexes a repository into a persistent knowledge graph of functions, classes, call chains, and cross-file relationships using `tree-sitter` across 158 languages, purely programmatically with no LLM in the indexing path, and the lesson cites a benchmark of roughly 3,400 tokens for five structural queries via the graph against roughly 412,000 tokens for the equivalent grep-and-read approach.

## Key Concepts

- Graph-based exploration is reported at roughly ten times fewer tokens than file-by-file reading across a 31-repository benchmark, while maintaining 83% answer quality.
- Purely programmatic indexing (tree-sitter, no LLM) makes full re-indexing cheap enough to run routinely, unlike an LLM-summarised index that would cost real inference budget per rebuild.
- A `PreToolUse` hook intercepts an agent's existing grep calls and injects graph context automatically, rather than depending on the agent choosing to invoke a separate specialised tool — the lesson's explicit design response to most code-search MCP servers going unused because agents default to their built-in tools.
- Six exposed tools: `get_architecture` (repository overview), `search_graph` (symbol lookup), `trace_path` (call-chain following), `detect_changes` (git diff mapped to affected symbols), `query_graph` (Cypher-like structural queries), and `get_code_snippet` (single-function extraction).

## Terminology

- Knowledge graph (codebase sense) — a persistent structural index of a repository's functions, classes, call chains, and cross-file relationships, queried directly instead of reconstructed from raw text on each request.
- Blast radius — the full set of symbols affected by a prospective code change, surfaced by graph traversal rather than estimated by manual inspection.

## Architecture and Implementation

A single install script (`curl ... | bash`, with a `--ui` flag for graph visualisation) auto-detects eleven coding agents and configures both the MCP entry and the `PreToolUse` hook automatically. On a worked case study (tracing a canvas lock, `createDesignDraftNode`, through a monorepo), the graph found all thirteen actual call sites where the lock could be affected at roughly 11,000 tokens, against roughly 38,000 tokens and zero call sites found by grepping alone — the lesson's sharpest illustration that grep's failure mode here is not slowness but a false negative that could ship a race condition.

## Code Examples

Two install commands (base install, and with `--ui` for the visualisation layer); no application code, since the tool itself is the deliverable.

## Best Practices

- Test the graph against one already-known dependency before trusting it broadly, to confirm it is navigating the actual codebase rather than guessing plausibly.
- Integrate indexing into a project's harness setup so every agent session starts with a current structural map, not a stale one.
- Run graph-based impact analysis before a change that touches a shared or load-bearing symbol, rather than relying on grep to surface every call site.

## Warnings and Anti-Patterns

- Relying on the model to consciously choose a specialised search tool over its built-in grep is, per the lesson, why most code-search MCP servers go unused; a hook that enriches the default tool is the more reliable design.
- Grep-only exploration is not merely slower than graph-based exploration on the cited case study — it returned zero of thirteen actual call sites, a false negative with direct correctness consequences, not just an efficiency cost.

## Related Concepts

- [[mcp]]
- [[memory]]
- [[claude-code]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson positions the tool as one component of a larger "codebase harness" — alongside local runtime setup, end-to-end test gates, and isolated parallel-work sandboxes — that a companion `/setup-codebase-harness` skill installs together, without expanding on the other components here.

## References

- Codebase Memory MCP: Give Your Coding Agent a Map (2026) — https://www.aibuilderclub.com/blog/codebase-memory-mcp-guide
