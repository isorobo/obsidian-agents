---
type: concept
status: draft
created: 2026-07-10
name: Agent vs LLM
slug: agent-vs-llm
topic:
- topic/foundations
- topic/concepts
tags:
- agents
- llm
- comparison
synonyms:
- agent versus language model
- agent vs model
defined_in: "[[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]"
related_concepts:
- "[[what-is-an-ai-agent]]"
- "[[the-agent-loop]]"
- "[[tool-use]]"
---

# Agent vs LLM

> A language model predicts text from a prompt; an agent wraps that model in a loop with tools and memory so it can act on the world.

## Summary

A bare language model answers in one shot. It reads a prompt and returns text. It holds no memory past the context window and touches nothing outside itself. An agent adds the parts the model lacks. It adds tools, a loop, and state. Anthropic calls the middle rung the augmented language model, a model enhanced with retrieval, tools, and memory. The agent runs that augmented model across many turns. The gap between model and agent is the gap between a function and a process.

## Key Concepts

- A language model maps a prompt to a text output in one pass.
- An agent runs the model across turns and acts through tools.
- The augmented language model bridges the two with retrieval, tools, and memory.
- Statefulness and action separate the agent from the model.

## Detail

A language model is stateless. Each call stands alone. The model cannot fetch a file, run code, or check a fact on its own. It generates the most probable continuation of the prompt. This power is real and bounded.

An agent removes the bounds through structure. Tools give the model hands. A loop gives the model turns. Memory gives the model recall past one context window. The model still generates text at the core. The agent turns that text into actions and feeds the results back. The model reasons; the harness acts and remembers.

## Trade-offs and Limits

A raw model wins on speed, cost, and simplicity for single-shot tasks. Summaries, rewrites, and classification need no loop. An agent wins where a task needs live data, tools, or many steps. The agent pays with latency, token cost, and failure modes the raw call never meets.

## Related

- [[what-is-an-ai-agent]]
- [[the-agent-loop]]
- [[tool-use]]
- [[memory]]

## Sources

- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]
- Effective context engineering for AI agents — https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

## See also

- [[MOC - Foundations]]
