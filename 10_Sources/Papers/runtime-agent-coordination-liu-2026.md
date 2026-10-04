---
type: source
status: draft
created: 2026-10-04
title: "Can AI Scientists Coordinate at Runtime?"
authors:
- Zijian Liu
- Yangzhixin Luo
- Junyu Lu
- Yi Li
- Yu Chen
- David Xu
- William F. Shen
- Xinchi Qiu
- Xisen Wang
organisation: arXiv preprint
source_type: paper
venue: arXiv
url: https://arxiv.org/abs/2610.00980
year: 2026
date_published: 2026-10-01
anthropic: false
topic:
- topic/multi-agent
- topic/research-papers
tags:
- runtime-coordination
- work-contracts
- verification
- ai-scientist
nlm_id:
nlm_skip: false
watchlist_channel: arxiv-agents
af_targets:
- af:DELEG-01
- af:RSCH-04/Q17
- af:RSCH-04/Q24
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 1268b14c1239fef8685a42ad7095223f11d2a78bb75eb878d0f147343f4c59df
---

# Can AI Scientists Coordinate at Runtime?

> Zijian Liu et al., "Can AI Scientists Coordinate at Runtime?", arXiv, 1 October 2026, https://arxiv.org/abs/2610.00980.

## Summary

The paper tests whether AI scientist agents can coordinate dynamically during execution instead of following a fixed workflow. It introduces Runtime Agent Coordination (RAC), which selects agents from existing AI-scientist hosts at run time, assigns scoped work contracts, and provides artifact-grounded verification. Across several benchmarks, runtime selection improved performance, while adding verification and contracts gave mixed results depending on host model and budget. Code is at https://github.com/systemind-team/Runtime-AI-Scientist (35 pages).

## Key Concepts

- Choose workers at run time rather than fixing the pipeline in advance.
- Scoped work contracts bound what each delegated agent does.
- Artifact-grounded verification checks outputs against produced artifacts.

## Terminology

- RAC: Runtime Agent Coordination.
- Host: an existing AI-scientist system whose agents RAC selects from.

## Architecture and Implementation

RAC sits above existing hosts: select agent, issue contract, verify artifact. It reuses hosts rather than replacing them.

## Code Examples

The source carries no reusable code on the abstract page; a repository is linked.

## Best Practices

- Scope delegated work with an explicit contract.
- Treat verification as a cost to be justified by budget and model.

## Warnings and Anti-Patterns

- Contracts and verification do not help uniformly; gains depended on host model and budget.

## Related Concepts

- [[supervisor-worker-multi-agent]]
- [[workflow-vs-autonomous-agent]]

## Future Work

Not stated on the abstract page.

## References

- https://arxiv.org/abs/2610.00980
- https://github.com/systemind-team/Runtime-AI-Scientist
