---
type: source
status: draft
created: 2026-10-04
title: "SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering"
authors:
- John Yang
- Carlos E. Jimenez
- Alexander Wettig
- Kilian Lieret
- Shunyu Yao
- Karthik Narasimhan
- Ofir Press
organisation: Princeton University
source_type: paper
venue: arXiv
url: https://arxiv.org/abs/2405.15793
year: 2024
date_published: 2024-05-06
anthropic: false
topic:
- topic/tool-use
- topic/research-papers
tags:
- swe-agent
- agent-computer-interface
- software-engineering
- swe-bench
nlm_id:
nlm_skip: false
watchlist_channel: af-corpus-papers
af_targets:
- af:RSCH-04/Q13
- af:RSCH-04/Q14
- af:RSCH-04/Q16
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: efc34189c5c6cd7e940c3f2b5b623f99e8656e20cdbaab233c53463d4f6dde82
---

# SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering

> John Yang, Carlos E. Jimenez, Alexander Wettig, Kilian Lieret, Shunyu Yao, Karthik Narasimhan and Ofir Press, "SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering", arXiv, 6 May 2024 (revised 11 November 2024), https://arxiv.org/abs/2405.15793.

## Summary

The paper studies how interface design shapes language-model agent performance. It introduces SWE-agent, which gives an LM agent a custom agent-computer interface (ACI) for creating and editing code files, navigating repositories and running tests. Per the abstract, SWE-agent reached pass@1 rates of 12.5% on SWE-bench and 87.7% on HumanEvalFix, well above earlier non-interactive LM approaches. The central claim is that deliberate interface design measurably changes agent behaviour and results. This note is based on the arXiv abstract page; the full text was not read.

## Key Concepts

- Agent-computer interface: an interface designed for the model, not for a human user.
- Interface design as a performance lever, independent of the model.
- Core ACI capabilities: file creation and editing, repository navigation, test execution.
- Interactive agents outperform non-interactive baselines on SWE-bench.

## Terminology

- ACI: agent-computer interface.
- SWE-bench: benchmark of real software engineering tasks.
- HumanEvalFix: code-repair benchmark.
- pass@1: share of tasks solved on the first attempt.

## Architecture and Implementation

The system wraps the computer environment in an ACI that exposes a small set of model-friendly operations for editing, navigating and testing code. Code, data and a demo are published at swe-agent.com. Command-level detail was not fetched.

## Code Examples

The source carries no reusable code on the abstract page.

## Best Practices

- Design the tool surface for the model, and treat it as a tuned component.
- Measure interface changes against a benchmark.

## Warnings and Anti-Patterns

- Reusing a human-oriented interface unchanged may limit agent performance, which is the paper's motivating observation.

## Related Concepts

- [[tool-use]]
- [[the-agent-loop]]
- [[what-is-an-ai-agent]]

## Future Work

The abstract does not state future work.

## References

- https://arxiv.org/abs/2405.15793
