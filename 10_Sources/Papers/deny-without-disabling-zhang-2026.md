---
type: source
status: draft
created: 2026-10-04
title: "Deny Without Disabling: Authorization-Paired Evaluation and Control for Multi-Agent Systems"
authors:
- Yunbei Zhang
- Saiyue Lyu
- Janet Wang
- Yingqiang Ge
- Jiang Guo
- Jihun Hamm
- Chandan K Reddy
organisation: arXiv preprint
source_type: paper
venue: arXiv
url: https://arxiv.org/abs/2610.00371
year: 2026
date_published: 2026-09-30
anthropic: false
topic:
- topic/security
- topic/multi-agent
- topic/research-papers
tags:
- authorization
- information-flow
- flowreview
- permissions
nlm_id:
nlm_skip: false
watchlist_channel: arxiv-agents
af_targets:
- af:DELEG-01
- af:RSCH-04/Q26
- af:ADR-0007
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 64a8da189868f5cd028f2b7f6a1b3cf62b064b5c80862575fb8a00dee3d4d087
---

# Deny Without Disabling: Authorization-Paired Evaluation and Control for Multi-Agent Systems

> Yunbei Zhang et al., "Deny Without Disabling: Authorization-Paired Evaluation and Control for Multi-Agent Systems", arXiv, 30 September 2026, https://arxiv.org/abs/2610.00371.

## Summary

The paper addresses a multi-agent safety gap: contributions that are admissible alone can jointly enable a prohibited use. The authors propose authorization-paired evaluation and FlowReview, a framework covering object resolution, permission ranking and deterministic enforcement. In controlled experiments, reviewing combined artifacts cut the denied-commit rate from 86.0% to zero with no loss of authorized supply. The central claim is that multi-agent safety needs governance of composed information flows while keeping legitimate collaboration. Code and data are at https://github.com/yunbeizhang/FlowReview (44 pages, 9 figures).

## Key Concepts

- Per-agent permission checks miss prohibited outcomes that emerge from composition.
- Evaluation should pair a denial test with an authorized-supply test, so safety is not bought by disabling the system.
- Enforcement is deterministic, not model-judged.

## Terminology

- Denied-commit rate: share of prohibited commits that get through.
- Authorized supply: legitimate contributions that still flow.
- FlowReview: the paper's review-and-enforce framework.

## Architecture and Implementation

FlowReview resolves the objects artifacts refer to, ranks permissions, and enforces the decision deterministically on combined artifacts rather than on each contribution alone.

## Code Examples

The source carries no reusable code on the abstract page; a repository is linked.

## Best Practices

- Review the combined artifact at the commit point, not only each agent's output.
- Report both denial and authorized-supply metrics.

## Warnings and Anti-Patterns

- Blanket denial scores well on safety and destroys utility; measure both.
- Isolated admissibility checks give false assurance.

## Related Concepts

- [[supervisor-worker-multi-agent]]
- [[evaluation]]

## Future Work

Not stated on the abstract page.

## References

- https://arxiv.org/abs/2610.00371
- https://github.com/yunbeizhang/FlowReview
