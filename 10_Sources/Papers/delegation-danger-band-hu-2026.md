---
type: source
status: draft
created: 2026-10-04
title: "The Delegation Danger Band: Why Mid-Capability Sub-Agents Over-Trust Inherited Stale State"
authors:
- Jundong Hu
- Shekar Ramachandran
organisation: arXiv preprint
source_type: paper
venue: arXiv
url: https://arxiv.org/abs/2610.00041
year: 2026
date_published: 2026-09-03
anthropic: false
topic:
- topic/multi-agent
- topic/memory
- topic/research-papers
tags:
- delegation
- context-inheritance
- sub-agents
- stale-state
nlm_id:
nlm_skip: false
watchlist_channel: arxiv-agents
af_targets:
- af:DELEG-01
- af:RSCH-04/Q25
- af:RSCH-04/Q12
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 25813894d8d627f802cf597d6ded798b9af6e326f6d0e51ce7f64bb3ff210229
---

# The Delegation Danger Band: Why Mid-Capability Sub-Agents Over-Trust Inherited Stale State

> Jundong Hu and Shekar Ramachandran, "The Delegation Danger Band: Why Mid-Capability Sub-Agents Over-Trust Inherited Stale State", arXiv, 3 September 2026, https://arxiv.org/abs/2610.00041.

## Summary

The paper studies agent frameworks that delegate to child agents by passing down the parent's context. It compares three inheritance policies (Reset, Selective, Full) across the Qwen3 model family on MuSiQue and HotpotQA. Deference to superseded state falls sharply as measured capability rises. Mid-capability models (Qwen3-1.7B) dip below their own baseline when they inherit the full context, which the authors call a "danger band". Selective handoff beat full inheritance, and a universal capability router did not work across datasets. The source is a preprint under review at a NeurIPS 2026 workshop, and the abstract page lists no code.

## Key Concepts

- Context inheritance is a design choice for delegation, not a free default.
- Stale or superseded state in inherited context can mislead a child agent.
- The harm depends on the child model's capability, with a mid-range worst case.
- Selective handoff of context outperformed passing everything.

## Terminology

- Danger band: the capability range where inherited stale state hurts more than starting clean.
- Inheritance policy: Reset (nothing), Selective (curated), Full (whole parent context).

## Architecture and Implementation

The study varies only what context a child receives when a parent delegates. It does not propose a new framework. Evidence comes from multi-hop question answering benchmarks with small open models.

## Code Examples

The source carries no reusable code.

## Best Practices

- Prefer curated handoff over copying the full parent context to a sub-agent.
- Test delegation at the capability level of the model you actually deploy.

## Warnings and Anti-Patterns

- Do not assume a router keyed on model capability fixes over-trust; it failed to generalise here.
- Results come from small models and QA tasks; transfer to coding agents is unproven.

## Related Concepts

- [[supervisor-worker-multi-agent]]
- [[memory]]

## Future Work

The abstract reports that a universal capability router was ineffective, leaving per-task policy selection open.

## References

- https://arxiv.org/abs/2610.00041
