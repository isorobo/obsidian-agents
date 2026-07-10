---
type: concept
status: draft
created: 2026-07-10
name: The Agent Loop
slug: the-agent-loop
topic:
- topic/foundations
- topic/architectures
tags:
- agents
- loop
- control-flow
synonyms:
- agentic loop
- agent execution loop
- perceive-decide-act loop
defined_in: "[[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]"
related_concepts:
- "[[what-is-an-ai-agent]]"
- "[[tool-use]]"
- "[[react]]"
---

# The Agent Loop

> The agent loop is the repeating cycle in which a model reads context, chooses an action, calls a tool, and reads the result until the task closes.

## Summary

The agent loop is the engine of every agent. Anthropic describes agents running in a loop, using tools based on environment feedback at each step. The environment returns ground truth, such as a tool result or code output. The model reads that truth, judges progress, and picks the next move. The loop ends at a stop condition or a human checkpoint. This cycle turns a one-shot model into a system that acts over time.

## Key Concepts

- The loop repeats read, decide, act, and observe.
- Environment feedback grounds each step in ground truth.
- A stop condition or checkpoint closes the loop.
- The loop carries state that a single model call lacks.

## Detail

The loop runs four moves. First, the model reads the current context and the goal. Second, the model decides the next action. Third, the harness runs the action as a tool call. Fourth, the environment returns a result that rejoins the context. The cycle then repeats with richer context.

ReAct names the pattern behind the loop. It interleaves reasoning traces with actions. The reasoning tracks the plan and handles exceptions. The action gathers information from the world. The loop needs a guard. A step budget or a goal test stops runaway cycles. A human checkpoint holds the loop at a blocker or a risky action.

## Trade-offs and Limits

The loop gives recovery, since the model reads each result and adjusts. It handles branches a fixed script cannot foresee. The loop can also stall, repeat, or drift on a hard task. Every turn adds tokens and latency. Guards and budgets keep the loop bounded and legible.

## Related

- [[what-is-an-ai-agent]]
- [[tool-use]]
- [[react]]
- [[planning-and-reasoning]]

## Sources

- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]
- ReAct: Synergizing Reasoning and Acting in Language Models — https://arxiv.org/abs/2210.03629

## See also

- [[MOC - Architectures]]
- [[MOC - Foundations]]
