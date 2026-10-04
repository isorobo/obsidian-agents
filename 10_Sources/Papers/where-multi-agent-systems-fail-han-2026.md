---
type: source
status: draft
created: 2026-10-04
title: "Where Do Multi-Agent Systems Fail? Evidence-Grounded Diagnosis of Collective Mechanisms"
authors:
- Zhengye Han
organisation: arXiv preprint
source_type: paper
venue: arXiv
url: https://arxiv.org/abs/2609.38761
year: 2026
date_published: 2026-09-30
anthropic: false
topic:
- topic/evaluation
- topic/multi-agent
- topic/research-papers
tags:
- failure-diagnosis
- diagnostic-contracts
- execution-records
- provenance
nlm_id:
nlm_skip: false
watchlist_channel: arxiv-agents
af_targets:
- af:ADR-0008
- af:RSCH-04/Q19
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: f2ab1eeb377e1e932f01adb0abb74866a9a431fa893a2e626f3e14e5b6fe35da
---

# Where Do Multi-Agent Systems Fail? Evidence-Grounded Diagnosis of Collective Mechanisms

> Zhengye Han, "Where Do Multi-Agent Systems Fail? Evidence-Grounded Diagnosis of Collective Mechanisms", arXiv, 30 September 2026, https://arxiv.org/abs/2609.38761.

## Summary

The paper asks how to find which collective mechanism of a multi-agent system has failed. Its key observation is that a system can return correct answers while breaking the rules for routing and storing information. The author introduces diagnostic contracts that separate a violation from the execution records that prove it. On four mechanisms, broken components often left answers intact. LLM diagnosers found more violations in internal records than in public outputs, and generic prompts often claimed unfounded certainty, reduced by stating contracts explicitly. Contracts applied narrowly to independently built systems, and near-perfect benchmark diagnosis degraded elsewhere. The paper concludes that a correct outcome does not replace records of how mechanisms operated. No code is linked.

## Key Concepts

- Outcome correctness is weak evidence about mechanism health.
- Diagnosis needs execution records, not only final outputs.
- Explicit contracts reduce unfounded certainty in LLM diagnosers.

## Terminology

- Diagnostic contract: a stated rule for a mechanism plus the records that evidence a violation.
- Collective mechanism: routing, storage or similar shared function in a multi-agent system.

## Architecture and Implementation

Four mechanisms were tested; diagnosers read internal records against contracts.

## Code Examples

The source carries no reusable code.

## Best Practices

- Log internal execution records so mechanism-level checks are possible.
- State the contract to the diagnoser instead of prompting generically.

## Warnings and Anti-Patterns

- Do not treat a passing answer as proof the system worked as designed.
- Contracts transferred poorly to independently developed systems.

## Related Concepts

- [[evaluation]]
- [[supervisor-worker-multi-agent]]

## Future Work

Not stated on the abstract page.

## References

- https://arxiv.org/abs/2609.38761
