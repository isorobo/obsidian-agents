---
type: source
status: draft
created: 2026-07-10
title: "ReAct: Synergizing Reasoning and Acting in Language Models"
authors:
- Shunyu Yao
- Jeffrey Zhao
- Dian Yu
- Nan Du
- Izhak Shafran
- Karthik Narasimhan
- Yuan Cao
organisation: Princeton University and Google Research
source_type: paper
venue: ICLR 2023
url: https://arxiv.org/abs/2210.03629
year: 2022
date_published: 2022-10-06
anthropic: false
topic:
- topic/architectures
- topic/research-papers
tags: [react, reasoning, tool-use, agent-loop]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# ReAct: Synergizing Reasoning and Acting in Language Models

> Yao, Zhao, Yu, Du, Shafran, Narasimhan, and Cao. "ReAct: Synergizing Reasoning and Acting in Language Models." ICLR 2023. arXiv:2210.03629. https://arxiv.org/abs/2210.03629

## Summary

The paper interleaves reasoning traces and task actions in one language model loop.
Reasoning traces plan and track the task. Actions query external sources such as a
Wikipedia API or an environment. The model reads each observation, then reasons again.
This loop grounds reasoning in fresh evidence and cuts hallucination. The authors test
ReAct on question answering, fact verification, and interactive decision tasks. ReAct
beats action-only and reason-only baselines and improves the trace a human can read.

## Key Concepts

- Interleaved thought, action, and observation as one prompt trace.
- Reasoning that guides which action to take next.
- Actions that fetch external knowledge to correct the reasoning.
- Human-readable traces that expose the model decision path.

## Terminology

- Thought — a reasoning step the model writes before acting.
- Action — a call to a tool or environment, such as search or lookup.
- Observation — the result the environment returns for an action.
- Trajectory — the full thought-action-observation sequence for a task.

## Architecture and Implementation

ReAct prompts the model to emit a thought, then an action, then to consume the
observation. The action space combines the task action set with a free-form reasoning
"action". Few-shot exemplars teach the format. The loop repeats until the model emits a
finish action. HotpotQA and FEVER use a Wikipedia search-and-lookup API. ALFWorld and
WebShop use the environment action set.

## Code Examples

The paper carries prompt exemplars for each task. Reference implementations exist in the
authors' released code and in agent frameworks that ship a ReAct loop.

## Best Practices

- Show few-shot exemplars in the thought-action-observation format.
- Combine ReAct with chain-of-thought self-consistency for hard reasoning.
- Ground each reasoning step in a fresh observation.

## Warnings and Anti-Patterns

- A wrong early action derails the whole trajectory.
- The model repeats an action when no new observation arrives.
- Long trajectories consume context and raise cost.

## Related Concepts

- [[react]]
- [[the-agent-loop]]
- [[tool-use]]
- [[planning-and-reasoning]]

## Future Work

The authors flag scaling to larger action spaces and combining ReAct with reinforcement
learning and fine-tuning.

## References

- https://arxiv.org/abs/2210.03629
