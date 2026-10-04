---
type: source
status: draft
created: 2026-07-11
title: "RAG vs Long Context vs Fine-Tuning: When Each Wins"
authors:
- Shirley
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 3.7
url: https://www.aibuilderclub.com/blog/rag-vs-long-context-vs-fine-tuning
year: 2026
date_published: 2026-06-12
anthropic: false
topic:
- topic/memory
tags:
- rag
- fine-tuning
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
af_targets:
- af:ADR-0005
- af:RSCH-04/Q12
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 95a474580c103a829327ee3f211104b2f5851007007e1fd7e70ee57d3c85cb30
---

# RAG vs Long Context vs Fine-Tuning: When Each Wins

> Shirley, "RAG vs Long Context vs Fine-Tuning: When Each Wins", AI Builder Club, Build AI Agents Course, 12 June 2026, https://www.aibuilderclub.com/blog/rag-vs-long-context-vs-fine-tuning.

## Summary

Three ways to get a model working knowledge it was not trained on, framed through an exam analogy: long context brings the whole textbook into the room, RAG has a librarian fetch only the relevant pages, and fine-tuning internalises the material during study beforehand. The lesson gives a decision table rather than a universal winner — static, small corpora stay in context directly; large or changing corpora that need citations go through RAG; changing the model's behaviour or style is what fine-tuning is actually for — and most production systems end up layering more than one.

## Key Concepts

- Decision rule: a static corpus under roughly 50K tokens belongs directly in context; a large or changing corpus that needs citations belongs in RAG; a need to change model behaviour or style belongs to fine-tuning; production systems typically combine all three.
- RAG solves two distinct LLM failure modes at once: a training-data knowledge cutoff and hallucination under genuine uncertainty.
- The modern RAG pipeline runs four stages: chunking (with "one chunk, one idea" as the governing principle), hybrid retrieval (vector search for paraphrase, BM25 keyword search for exact terms such as product codes, merged), reranking (a cheap-then-expensive two-pass architecture, described as typically improving quality more than swapping the embedding model), and assembly with an explicit "answer only from the provided sources" instruction to stop the model padding retrieval gaps with invented detail.
- Classic 2023-style fixed chunk-and-embed RAG is losing ground to agentic retrieval, where the model is given search tools and iteratively searches, reads, and refines its own query — slower and more token-hungry, but better on complex, messy document sets.

## Terminology

- Chunking — splitting source documents into retrievable units before embedding; the lesson's stated highest-leverage decision in the whole pipeline.
- HyDE (Hypothetical Document Embeddings) — a query-rewriting technique where the model drafts a plausible (if wrong) answer first, then embeds that answer-shaped text to search, since embedding proximity tracks surface shape more than truth.
- Reranking — a second, more expensive pass where a cross-encoder re-scores the top candidates from an initial retrieval by reading the query and each chunk together.
- Agentic retrieval — giving the model retrieval as a tool (search, read, refine, search again) instead of retrieving once upfront and handing over the results.

## Architecture and Implementation

A concrete Next.js/Supabase starting stack: store embeddings in Postgres with `pgvector`, convert source documents to Markdown and apply structure-aware chunking at roughly 800 tokens, run hybrid retrieval via `pgvector` cosine similarity combined with Postgres full-text search, and generate from the top five labelled chunks with a source-grounding instruction. The lesson recommends measuring actual failure points on this baseline before adding reranking or query rewriting, rather than building both in from the start.

## Code Examples

None as runnable code; the lesson works at the level of pipeline architecture and a named technology stack rather than a worked program.

## Best Practices

- Treat chunking as the single highest-leverage decision in a RAG system, ahead of embedding-model choice.
- Add reranking before swapping the embedding model when retrieval quality is the complaint; it typically moves the needle more.
- Instruct the model explicitly to answer only from provided sources and to say so when the sources do not cover the question, to prevent fluent hallucination from masquerading as a grounded answer.
- Build the simple hybrid-retrieval baseline first and add reranking or query rewriting only once a measured failure justifies the added complexity.

## Warnings and Anti-Patterns

- Reaching for RAG on a small, static corpus adds retrieval infrastructure and latency a direct-context approach would have avoided entirely.
- Classic fixed chunk-and-embed RAG has a documented failure pattern on messy, unstructured document sets: fragments losing surrounding context and no way to recover from a poor initial retrieval.
- Skipping the explicit "say so if the sources do not cover it" instruction lets a model fill retrieval gaps with fluent, unlabelled invention.

## Related Concepts

- [[memory]]
- [[claude-code]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson flags agentic retrieval, exemplified by Claude Code's grep-and-targeted-read pattern in place of a vector index, as the pattern worth watching as it matures, without a full worked implementation.

## References

- RAG vs Long Context vs Fine-Tuning: When Each Wins — https://www.aibuilderclub.com/blog/rag-vs-long-context-vs-fine-tuning
