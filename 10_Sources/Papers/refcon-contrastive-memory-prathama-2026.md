---
type: source
status: draft
created: 2026-10-04
title: "RefCon: Iterative Refinement and Contrastive Memory Extraction for Context-Evolving Agent"
authors:
- Ubaidillah Ariq Prathama
- Bo Liu
- Yeo Boon Hong
- Yu-Xuan Huang
- Yangkai Ding
- Tao Yu
organisation: arXiv preprint
source_type: paper
venue: arXiv
url: https://arxiv.org/abs/2609.39143
year: 2026
date_published: 2026-09-30
anthropic: false
topic:
- topic/memory
- topic/research-papers
tags:
- agent-memory
- memory-extraction
- self-refinement
- self-contrast
nlm_id:
nlm_skip: false
watchlist_channel: arxiv-agents
af_targets:
- af:ADR-0005
- af:RSCH-04/Q11
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 5649772bfec54e3dbf9c5809d51a69817697fce81a3e63586f5a7cf1ca1bc707
---

# RefCon: Iterative Refinement and Contrastive Memory Extraction for Context-Evolving Agent

> Ubaidillah Ariq Prathama et al., "RefCon: Iterative Refinement and Contrastive Memory Extraction for Context-Evolving Agent", arXiv, 30 September 2026, https://arxiv.org/abs/2609.39143.

## Summary

RefCon extracts high-quality memories from long-horizon agent interactions without labelled data. It merges sequential self-refinement with parallel self-contrast. The abstract reports gains of 21.6% on ACE and 16.6% on ReMe over baselines. A variant, DivCon, does better on some datasets, and the method works across model sizes and task domains, including software engineering. The abstract page shows no code link and no venue.

## Key Concepts

- Memory quality is the bottleneck for context-evolving agents.
- Refine a memory in sequence, and contrast several candidates in parallel.
- No labels are needed for extraction.

## Terminology

- Context-evolving agent: an agent whose stored context grows from its own interactions.
- Contrastive extraction: comparing parallel attempts to pick out what is useful.

## Architecture and Implementation

Memories are distilled from interaction trajectories by iterative refinement and by contrasting parallel extractions.

## Code Examples

The source carries no reusable code.

## Best Practices

- Treat memory extraction as a step worth its own refinement and comparison, not a single summarise call.

## Warnings and Anti-Patterns

- Reported gains are relative to the paper's baselines and benchmarks; abstract-only evidence here.

## Related Concepts

- [[memory]]
- [[the-agent-loop]]

## Future Work

Not stated on the abstract page.

## References

- https://arxiv.org/abs/2609.39143
