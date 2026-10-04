---
type: source
status: draft
created: 2026-10-04
title: "Mid-Harness: Scaling Actions Between Model and Harness for Terminal Agents"
authors:
- Minki Kang
- Ryo Hachiuma
- Shaokun Zhang
- Subhashree Radhakrishnan
- Yonggan Fu
- Jindong Jiang
- Mingjie Liu
- Ehsan Hosseini-Asl
- Yi Dong
- Yu-Chiang Frank Wang
- Byung-Kwan Lee
organisation: arXiv preprint
source_type: paper
venue: arXiv
url: https://arxiv.org/abs/2609.39982
year: 2026
date_published: 2026-09-30
anthropic: false
topic:
- topic/architectures
- topic/tool-use
- topic/research-papers
tags:
- harness
- terminal-agents
- action-scaling
- verifier
nlm_id:
nlm_skip: false
watchlist_channel: arxiv-agents
af_targets:
- af:ADR-0004
- af:RSCH-04/Q14
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 816a5cb19bbd051b0eab42e6d39b931e84fc5b228f823b00f672dcd459c26c37
---

# Mid-Harness: Scaling Actions Between Model and Harness for Terminal Agents

> Minki Kang et al., "Mid-Harness: Scaling Actions Between Model and Harness for Terminal Agents", arXiv, 30 September 2026, https://arxiv.org/abs/2609.39982.

## Summary

The paper asks whether spending compute at the model-harness interface makes terminal agents more reliable. Mid-Harness samples several candidate actions and validates them before execution. The authors report that a capable verifier can exploit useful alternatives from the same generator, lifting Pass@1 on TerminalBench-Lite from 50% to 68.03%. They frame this as action scaling, a form of test-time compute applied per step. A project page is at https://byungkwanlee.github.io/MidHarness-page/; the abstract page shows no code repository.

## Key Concepts

- The harness can sit between proposal and execution and check actions first.
- Sampling multiple actions per step plus a verifier is a test-time compute lever.
- Verifier quality bounds the gain.

## Terminology

- Action scaling: sampling and validating candidate actions before execution.
- Terminal agent: an agent acting through a shell.

## Architecture and Implementation

The design adds a sample-then-validate stage in the harness between the model's proposed action and its execution in the terminal.

## Code Examples

The source carries no reusable code on the abstract page.

## Best Practices

- Validate actions in the harness before they run, especially for irreversible shell commands.

## Warnings and Anti-Patterns

- Extra sampling costs tokens and latency per step; the gain depends on a strong verifier.

## Related Concepts

- [[the-agent-loop]]
- [[tool-use]]

## Future Work

Not stated on the abstract page.

## References

- https://arxiv.org/abs/2609.39982
- https://byungkwanlee.github.io/MidHarness-page/
