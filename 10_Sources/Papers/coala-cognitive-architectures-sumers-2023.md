---
type: source
status: draft
created: 2026-10-04
title: "Cognitive Architectures for Language Agents"
authors:
- Theodore R. Sumers
- Shunyu Yao
- Karthik Narasimhan
- Thomas L. Griffiths
organisation: Princeton University
source_type: paper
venue: Transactions on Machine Learning Research
url: https://arxiv.org/abs/2309.02427
year: 2023
date_published: 2023-09-05
anthropic: false
topic:
- topic/architectures
- topic/research-papers
tags:
- coala
- cognitive-architecture
- language-agents
- action-space
- memory
nlm_id:
nlm_skip: false
watchlist_channel: af-corpus-papers
af_targets:
- af:RSCH-04/Q01
- af:RSCH-04/Q03
- af:RSCH-04/Q11
- af:RSCH-04/Q30
- af:RSCH-04/Q31
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: b640acde8493ecab599994d198410b0f1d14b850c3f2df7569689ab36d485f1e
---

# Cognitive Architectures for Language Agents

> Theodore R. Sumers, Shunyu Yao, Karthik Narasimhan and Thomas L. Griffiths, "Cognitive Architectures for Language Agents", Transactions on Machine Learning Research (arXiv v1 5 September 2023, v3 March 2024), https://arxiv.org/abs/2309.02427.

## Summary

The paper introduces CoALA, a framework for organising existing language agents and planning future ones. It draws on cognitive science and symbolic AI and describes an agent through modular memory, a structured action space and a decision-making process. The authors survey recent language-agent work through this lens and propose research directions, positioning current agents in the history of AI. The TMLR camera-ready version has 19 pages of main content. This note is based on the arXiv abstract page; the full text was not read.

## Key Concepts

- One framework to describe many agents in common terms.
- Modular memory as a first-class component.
- A structured action space (per the abstract, not detailed here).
- A decision-making process that selects actions.
- Placement of LLM agents within cognitive-architecture history.

## Terminology

- Language agent: an LLM-based agent using external tools or internal reasoning chains.
- CoALA: Cognitive Architectures for Language Agents.

## Architecture and Implementation

The framework is conceptual: memory modules, action spaces and a decision procedure are the three axes for describing any agent. It is a descriptive taxonomy, not a runtime. Finer detail was not fetched.

## Code Examples

The source carries no reusable code on the abstract page.

## Best Practices

- Describe an agent by its memory, action space and decision process before comparing implementations.
- Use a shared vocabulary so different agents can be compared.

## Warnings and Anti-Patterns

- A taxonomy does not itself show which abstractions are universal and which are implementation patterns; that judgement remains with the reader.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[memory]]
- [[the-agent-loop]]
- [[react]]

## Future Work

The paper suggests future research directions and a path towards language-based general intelligence; specifics were not fetched.

## References

- https://arxiv.org/abs/2309.02427
