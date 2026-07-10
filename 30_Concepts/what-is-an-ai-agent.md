---
type: concept
status: draft
created: 2026-07-10
name: What Is an AI Agent
slug: what-is-an-ai-agent
topic:
- topic/foundations
- topic/concepts
tags:
- agents
- definition
synonyms:
- AI agent
- autonomous agent
- LLM agent
defined_in: "[[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]"
related_concepts:
- "[[agent-vs-llm]]"
- "[[the-agent-loop]]"
- "[[workflow-vs-autonomous-agent]]"
---

# What Is an AI Agent

> An AI agent is a system where a language model directs its own process and tool use to accomplish a task.

## Summary

An AI agent turns a language model into an actor. The model reads a goal, chooses an action, calls a tool, and reads the result. It repeats this cycle until the task closes. Anthropic frames the agent against the workflow. A workflow follows fixed code paths. An agent controls its own path. This control gives flexibility and carries cost. The definition matters because it sets the design bar for the whole field.

## Key Concepts

- The model holds control over how it accomplishes the task.
- The agent acts through tools and reads feedback from an environment.
- Autonomy separates an agent from a scripted workflow.
- The augmented language model forms the base building block.

## Detail

An agent needs three parts. It needs a model that plans and decides. It needs tools that reach the outside world. It needs a loop that carries state across steps. The model receives a goal in natural language. It selects an action and emits a tool call. The environment runs the tool and returns ground truth. The model reads the result and picks the next action.

Autonomy sets the boundary. A workflow author fixes each step in code. An agent selects each step at run time. This choice raises capability on open tasks. It also raises risk, cost, and the burden of oversight. Anthropic advises the simplest design that solves the task.

## Trade-offs and Limits

Agents suit open tasks where the path resists a fixed script. They handle branching and recovery that a workflow cannot foresee. They cost more tokens, more latency, and more supervision. A fixed workflow beats an agent on a narrow, stable task.

## Related

- [[agent-vs-llm]]
- [[the-agent-loop]]
- [[tool-use]]
- [[workflow-vs-autonomous-agent]]

## Sources

- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]
- ReAct: Synergizing Reasoning and Acting in Language Models — https://arxiv.org/abs/2210.03629

## See also

- [[MOC - Foundations]]
