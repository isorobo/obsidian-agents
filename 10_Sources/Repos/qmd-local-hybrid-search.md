---
type: source
status: draft
created: 2026-07-11
title: "qmd: Query Markup Documents"
authors:
- tobi
organisation: tobi (GitHub)
source_type: repo
venue: GitHub
url: https://github.com/tobi/qmd
year: 2026
date_published:
anthropic: false
topic:
- topic/memory
- topic/mcp
tags:
- local-search
- rag
- obsidian
nlm_id:
nlm_skip: false
watchlist_channel:
af_targets:
- af:DELEG-02
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: b19ac1c2dd2580e2a1a79947e65adbacc0cc5b532f19c3a8ad86ace288fb2782
---

# qmd: Query Markup Documents

> tobi, "qmd", GitHub repository, https://github.com/tobi/qmd. MIT licence.

## Summary

`qmd` is a local, on-device search engine purpose-built for markdown vaults, meeting notes, and other personal document stores — the same tool Andrej Karpathy names as the recommended search layer once an LLM-maintained wiki grows past a few hundred pages, per [[10_Sources/Blog/karpathy-llm-wiki-pattern|the vault's earlier Karpathy LLM Wiki note]]. It combines keyword search, vector search, and an LLM re-ranking pass into one hybrid pipeline, indexes entirely on the user's own machine, and exposes itself to LLM clients as an MCP server rather than requiring a bespoke integration per tool.

## Key Concepts

- Hybrid retrieval, not single-method search: BM25 full-text search (SQLite FTS5) for exact-term matches, local GGUF-model vector embeddings for paraphrase-level matches, and a cross-encoder LLM re-ranking pass over the merged candidates.
- Reciprocal Rank Fusion (RRF, k=60) merges the BM25 and vector result lists before reranking, with "position-aware blending" that weights raw retrieval score at 75% for the top three results and progressively trusts the reranker more further down the list — a deliberate defence against RRF diluting an exact keyword match that a paraphrase-expanded query would otherwise bury.
- Documents are chunked at roughly 900 tokens with 15% overlap using boundary-aware splitting that keeps code blocks intact, with optional tree-sitter AST parsing to prefer function and class boundaries as break points in source code.
- A `context` annotation layer lets the vault owner attach a hand-written description to a path (`qmd context add qmd://<path> "<description>"`), which the tool's own documentation calls its key feature for letting an LLM make better contextual choices about which document to fetch.

## Terminology

- Reciprocal Rank Fusion (RRF) — a method for merging ranked result lists from different retrieval methods (here, BM25 and vector search) into one combined ranking.
- Cross-encoder reranking — a second-pass model that scores a query and a candidate document together, rather than comparing independently computed embeddings, for a more precise but more expensive relevance judgement.
- Position-aware blending — qmd's specific RRF-plus-reranker weighting scheme, where trust in the reranker's score increases for lower-ranked candidates and decreases for top-ranked ones.

## Architecture and Implementation

Built primarily in TypeScript, running on Node.js 22-plus or Bun, using `node-llama-cpp` for local GGUF-model inference so both the embedding and reranking steps run without a cloud API call. Three search commands expose the pipeline at different depths: `qmd search` (BM25 only), `qmd vsearch` (vector only), and `qmd query` (the full hybrid pipeline with reranking). Retrieval commands (`qmd get`, `qmd multi-get`, `qmd ls`) fetch documents by path, docid, or glob once a relevant hit is found. `qmd init` creates a project-local index; `qmd collection add <path> --name <name>` registers a directory (default glob `**/*.md`, though arbitrary patterns are supported) for indexing; `qmd update` re-indexes and `qmd embed` regenerates vectors, with an `--chunk-strategy auto` flag enabling the AST-aware code chunking. The project ships both an MCP server (stdio or HTTP transport, HTTP defaulting to `localhost:8181`) exposing `query`, `get`, `multi_get`, and `status` as callable tools, and a TypeScript SDK (`createStore()`) for embedding the index directly into another program.

## Code Examples

CLI indexing and query commands (`qmd collection add`, `qmd query "..."`, `qmd context add`), and a minimal SDK usage snippet instantiating a store and calling `store.search()` programmatically.

## Best Practices

- Use `qmd query` (the full hybrid-plus-rerank pipeline) for actual retrieval decisions; treat `qmd search` and `qmd vsearch` as diagnostic tools for understanding why a result did or did not surface.
- Annotate high-value paths with `qmd context add` descriptions; the tool's own documentation frames this as the main lever for improving an LLM's document-selection accuracy, not the search algorithm itself.
- Enable AST-aware chunking (`--chunk-strategy auto`) specifically for source-code collections, not prose vaults, where it has no equivalent benefit.

## Warnings and Anti-Patterns

None stated explicitly in the README; the general RAG caution already captured in [[10_Sources/Blog/rag-vs-long-context-vs-fine-tuning|the vault's RAG vs long context vs fine-tuning note]] applies — retrieval quality depends on chunking and reranking discipline, not on installing the tool alone.

## Related Concepts

- [[memory]]
- [[mcp]]
- [[20_People/andrej-karpathy/profile|Andrej Karpathy]]

## Future Work

The README does not document authentication, multi-user, or remote-hosting considerations for the HTTP MCP transport; worth checking directly before exposing it beyond `localhost`.

## References

- qmd (GitHub repository) — https://github.com/tobi/qmd
