---
type: source
status: draft
created: 2026-07-10
title: Building Effective Agents
authors:
- Erik Schluntz
- Barry Zhang
organisation: Anthropic
source_type: blog
venue: Anthropic Engineering
url: https://www.anthropic.com/research/building-effective-agents
year: 2024
date_published: 2024-12-19
anthropic: true
topic:
- topic/foundations
- topic/agent-patterns
tags:
- agents
- workflows
- augmented-llm
nlm_id: 
nlm_skip: false
watchlist_channel: anthropic-engineering
---

# Building Effective Agents

> Erik Schluntz and Barry Zhang, "Building Effective Agents", Anthropic Engineering, 19 December 2024, https://www.anthropic.com/research/building-effective-agents.

## Summary

Anthropic distils lessons from building agents with customers across many industries. The post draws one line that governs the field. A workflow orchestrates language models and tools through fixed code paths. An agent lets the model direct its own process and tool use. The augmented language model forms the base building block for both.

## Key Concepts

- An agent is a system where the model directs its own process and tool use.
- A workflow runs the model and tools along predefined code paths.
- The augmented language model adds retrieval, tools, and memory to the base model.
- Simple, composable patterns beat heavy frameworks for most tasks.

## Terminology

- Agent — a system where the model dynamically directs its own processes and tool usage.
- Workflow — a system where the model and tools follow predefined code paths.
- Augmented LLM — a model enhanced with retrieval, tools, and memory.

## Architecture and Implementation

The post names one building block and five workflow patterns. The building block is the augmented language model. The patterns are prompt chaining, routing, parallelisation, orchestrator-workers, and evaluator-optimiser. Agents sit past the patterns. An agent runs the model in a loop, calls tools, and reads environment feedback at each step. The environment returns ground truth, such as tool results or code output. The agent pauses at checkpoints or blockers for human review.

## Code Examples

The post links a companion cookbook with reference implementations of each pattern.

## Best Practices

- Start with the simplest solution that works.
- Add agentic complexity only when it earns its cost.
- Design and document the tool interface with care.
- Keep the agent transparent so its plan stays legible.

## Warnings and Anti-Patterns

- Framework abstraction hides the prompt and the loop, which blocks debugging.
- Complex agents raise cost and latency without matching gains.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[agent-vs-llm]]
- [[the-agent-loop]]
- [[workflow-vs-autonomous-agent]]

## Future Work

The post flags reliability across long horizons and tool design as open ground.

## References

- Building Effective Agents — https://www.anthropic.com/research/building-effective-agents
- Writing effective tools for AI agents — https://www.anthropic.com/engineering/writing-tools-for-agents
