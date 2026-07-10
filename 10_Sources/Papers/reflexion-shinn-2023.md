---
type: source
status: draft
created: 2026-07-10
title: "Reflexion: Language Agents with Verbal Reinforcement Learning"
authors:
- Noah Shinn
- Federico Cassano
- Edward Berman
- Ashwin Gopinath
- Karthik Narasimhan
- Shunyu Yao
organisation: Northeastern University and Princeton University
source_type: paper
venue: NeurIPS 2023
url: https://arxiv.org/abs/2303.11366
year: 2023
date_published: 2023-03-20
anthropic: false
topic:
- topic/architectures
- topic/research-papers
tags: [reflexion, self-critique, memory, reinforcement]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Reflexion: Language Agents with Verbal Reinforcement Learning

> Shinn, Cassano, Berman, Gopinath, Narasimhan, and Yao. "Reflexion: Language Agents with Verbal Reinforcement Learning." NeurIPS 2023. arXiv:2303.11366. https://arxiv.org/abs/2303.11366

## Summary

Reflexion turns task feedback into written self-critique the agent stores and reuses.
The agent attempts a task, receives a feedback signal, and writes a reflection on the
failure. It holds that reflection in an episodic memory buffer. The next attempt reads
the reflection and adjusts. No weight update occurs; the language of the reflection
carries the learning. Reflexion reaches 91% pass@1 on HumanEval, above the reported
GPT-4 score of 80%. The method suits code, reasoning, and decision tasks.

## Key Concepts

- Verbal reinforcement in place of gradient updates.
- A reflection step that names why an attempt failed.
- An episodic memory buffer that carries reflections across trials.
- A separation of the actor, the evaluator, and the self-reflection roles.

## Terminology

- Actor — the model that produces actions for the task.
- Evaluator — the component that scores an attempt.
- Self-reflection — the model that writes a critique from the score and the trace.
- Episodic memory — the store of reflections read on the next trial.

## Architecture and Implementation

Reflexion wraps a base agent, often a ReAct actor, in a trial loop. The actor runs a
trajectory. The evaluator produces a reward or a test result. The self-reflection model
converts that signal and the trajectory into a short lesson. The lesson enters memory.
The next trial prepends the lesson to the prompt. The loop repeats to a trial budget or
a success signal.

## Code Examples

The paper ships reference code for HumanEval, ALFWorld, and HotpotQA experiments. Agent
frameworks reuse the actor, evaluator, and reflection split.

## Best Practices

- Keep reflections short and specific to the failure.
- Cap the memory buffer to hold the most useful lessons.
- Pair Reflexion with a reliable evaluator, such as unit tests.

## Warnings and Anti-Patterns

- A weak evaluator produces a misleading reflection.
- Many trials raise cost and latency.
- A vague reflection fails to change the next attempt.

## Related Concepts

- [[reflexion]]
- [[memory]]
- [[react]]
- [[the-agent-loop]]

## Future Work

The authors flag richer memory structures and stronger evaluators for tasks that lack a
clear reward.

## References

- https://arxiv.org/abs/2303.11366
