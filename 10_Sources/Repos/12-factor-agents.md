---
type: source
status: draft
created: 2026-10-04
title: "12-Factor Agents"
authors:
- Dex Horthy
organisation: HumanLayer
source_type: repo
venue: GitHub
url: https://github.com/humanlayer/12-factor-agents
year: 2025
date_published: 2025-03-30
anthropic: false
topic:
- topic/best-practices
- topic/architectures
tags:
- 12-factor-agents
- production-agents
- context-engineering
- control-flow
nlm_id:
nlm_skip: false
watchlist_channel: af-corpus-repos
af_targets:
- af:RSCH-01/12-factor-agents
- af:ADR-0005
- af:ADR-0007
- af:RSCH-04/Q22
- af:RSCH-04/Q28
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 4ab06949126dddc5ee44e5ce4b7fc8bf2ca28cfb12063a664d16d7ba6bf24b59
---

# 12-Factor Agents

> Dex Horthy, "12-Factor Agents", HumanLayer, 30 March 2025, https://github.com/humanlayer/12-factor-agents.

## Summary

The repository sets out twelve principles for building LLM-powered software that is good enough for production customers, modelled on the 12 Factor App methodology. It opens with a short history of DAGs, orchestrators and agent loops, then gives one document per factor. Its central argument is that most products called agents are deterministic code with LLM steps placed carefully, and that framework-first builds tend to stall at 70 to 80 percent quality. The author recommends adding small modular agent ideas to existing software rather than rewriting around a framework. The repository was created on 30 March 2025 and last pushed on 21 September 2025 (fetched from the GitHub API this run). Content is licensed CC BY-SA 4.0 and code Apache 2.0, per the README.

## Key Concepts

- Natural language to tool calls: the LLM's job is to emit structured function invocations.
- Own your prompts and your context window: do not hand either to a framework.
- Tools are just structured outputs; the code that acts on them is ordinary code.
- Unify execution state and business state into one source of truth.
- Launch, pause and resume through simple APIs; contact humans through tool calls.
- Own your control flow; compact errors into the context window.
- Prefer small, focused agents; trigger from anywhere; model the agent as a stateless reducer.

## Terminology

- Factor: one numbered design principle, each with its own document.
- Stateless reducer: the agent as a pure function from state and event to new state.
- Context window ownership: deciding exactly what the model sees each step.

## Architecture and Implementation

The README reduces the agent to an event-accumulating loop in which the model chooses the next step from the context, the code executes it, and the result is appended. Control flow, state and persistence stay in the application, not in a framework.

## Code Examples

```
context = [initial_event]
while True:
  next_step = await llm.determine_next_step(context)
  if next_step.intent === "done": return next_step.final_answer
  result = await execute_step(next_step)
  context.append(result)
```

## Best Practices

- Keep deterministic code deterministic and use the LLM only where judgement is needed.
- Treat human approval as a tool call so it fits the same control flow.
- Make runs pausable and resumable by keeping state outside the model call.
- Keep agents narrow in scope.

## Warnings and Anti-Patterns

- Adopting a framework that takes over prompts, context or control flow.
- Greenfield rewrites where incremental adoption would work.
- Letting raw error traces flood the context window.

## Related Concepts

- [[the-agent-loop]]
- [[workflow-vs-autonomous-agent]]
- [[tool-use]]
- [[memory]]

## Future Work

The README points to related resources and community contributors; individual factor documents are candidates for separate notes.

## References

- https://github.com/humanlayer/12-factor-agents
