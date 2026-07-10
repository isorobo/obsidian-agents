---
type: concept
status: draft
created: 2026-07-10
name: Planning and Reasoning
slug: planning-and-reasoning
topic:
- topic/planning
- topic/foundations
tags:
- planning
- reasoning
- chain-of-thought
synonyms:
- reasoning and planning
- agent planning
- task decomposition
defined_in: "[[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]"
related_concepts:
- "[[the-agent-loop]]"
- "[[react]]"
- "[[what-is-an-ai-agent]]"
---

# Planning and Reasoning

> Planning and reasoning are the model behaviours that break a goal into steps and decide the next action from the current state.

## Summary

An agent needs a plan to act well. Reasoning lets the model think through a problem before it answers. Planning lets the model break a goal into ordered steps. Chain-of-thought prompting showed that intermediate steps raise performance on hard tasks. ReAct joined reasoning to action, so the model plans and acts in one loop. Plan-and-execute split the two, so a planner sets steps and a worker runs them. These behaviours turn a goal into a sequence an agent can follow.

## Key Concepts

- Reasoning generates intermediate steps before the final answer.
- Planning decomposes a goal into an ordered set of actions.
- Chain-of-thought raises accuracy on arithmetic and multi-step tasks.
- ReAct interleaves reasoning with action inside the loop.

## Detail

Reasoning came first. Chain-of-thought prompting adds worked steps to the prompt. The model then reasons step by step and reaches a better answer on complex tasks. The steps also expose the model's path, which aids review.

Planning builds on reasoning. ReAct interleaves a reasoning trace with each action. The trace tracks the plan and handles exceptions; the action gathers ground truth. Plan-and-execute separates the roles. A planner drafts the full sequence up front. A worker executes each step and reports back. A replan step revises the plan when a result breaks it. Reflexion adds a critique that feeds the next attempt.

## Trade-offs and Limits

Explicit reasoning raises accuracy and legibility on hard, multi-step tasks. It costs tokens and can invent a false chain that reads as sound. Up-front planning gives structure but grows brittle when the world shifts. A tight replan loop keeps a plan alive against surprise.

## Related

- [[the-agent-loop]]
- [[react]]
- [[plan-and-execute]]
- [[reflexion]]

## Sources

- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]
- Chain-of-Thought Prompting Elicits Reasoning in Large Language Models — https://arxiv.org/abs/2201.11903
- ReAct: Synergizing Reasoning and Acting in Language Models — https://arxiv.org/abs/2210.03629

## See also

- [[MOC - Planning]]
