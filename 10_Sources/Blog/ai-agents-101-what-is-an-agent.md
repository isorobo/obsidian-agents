---
type: source
status: draft
created: 2026-07-11
title: "What Is an AI Agent? (AI Agents 101, Part 1)"
authors:
- AI Builder Club
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 1.2
url: https://www.aibuilderclub.com/blog/ai-agents-101-part-1
year: 2026
date_published: 2026-04-10
anthropic: false
topic:
- topic/foundations
tags:
- agent-loop
- tool-use
- course
nlm_id:
nlm_skip: false
watchlist_channel:
---

# What Is an AI Agent? (AI Agents 101, Part 1)

> AI Builder Club, "What Is an AI Agent? (AI Agents 101, Part 1)", Build AI Agents Course, 10 April 2026 (updated 11 June 2026), https://www.aibuilderclub.com/blog/ai-agents-101-part-1.

## Summary

Part 1 of a five-part course opens the definition every later lesson builds on. An agent is a software loop that uses a language model to decide what to do next, does it, checks the result, and decides again until the goal is reached. A chatbot answers once and stops; an agent pursues a multi-step objective through repeated action and observation on an identical underlying model. The lesson names four components every agent needs — the brain, tools, memory, and the loop — and walks the reader through a roughly 40-line reference implementation in both the Anthropic and OpenAI APIs.

## Key Concepts

- An agent is a loop: decide, act, observe, decide again, until the goal is reached.
- The architectural wrapper, not the model, separates an agent from a chatbot.
- Four components recur in every agent: the brain (LLM), tools, memory, and the loop (orchestrator).
- Native structured tool-calling supersedes string-based output parsing.
- Security in an agent lives in tool selection — which actions a tool exposes — not in the execution environment.

## Terminology

- Agent — a software loop that uses an LLM to decide the next action, executes it, observes the result, and repeats until the goal is met.
- The brain — the LLM component that evaluates state and selects an action but never executes it directly.
- The loop (orchestrator) — the code that sends state to the model, executes its chosen tool, and feeds the result back.

## Architecture and Implementation

The reference agent registers tools in a `TOOLS` dictionary mapping names to functions and JSON schemas. The loop sends the current messages and tool schemas to the model on each turn, checks for an `end_turn` stop reason, executes the requested tool if the model is not done, and appends the tool result to the message history before looping again, bounded by `max_steps`. The OpenAI variant differs only in schema wrapping (`{"type": "function"}`) and result-message role; the orchestration pattern is identical across providers.

## Code Examples

The lesson provides a complete, copy-paste agent (`list_files`, `read_file` tools plus the loop) runnable against either the Anthropic or the OpenAI API, and three graded exercises: add a `write_file` tool, add a constraining system prompt, and remove the `max_steps` guard on an unsolvable task to observe runaway behaviour before restoring it.

## Best Practices

- One tool, one job — decompose monolithic tools into focused, chainable ones.
- Always return tool results to the model; omitting the result feedback causes blind repetition.
- Always set `max_steps`; start at 10 and raise only when justified.
- Log every tool call — name, inputs, outputs, and the model's decision — for replay debugging.
- Start simple; add vector databases or multi-agent orchestration only after hitting a real limit.
- Use native structured tool-calling, never regex or string parsing of model output.

## Warnings and Anti-Patterns

- An unguarded loop can consume thousands of dollars in API cost before anyone notices.
- Withholding tool results from the model's context produces an agent blind to its own actions.
- Monolithic, multi-purpose tools raise argument-selection errors.
- Adding infrastructure (vector stores, multi-agent layers) before the simple version fails obscures rather than solves the problem.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[agent-vs-llm]]
- [[the-agent-loop]]
- [[tool-use]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson defers persistent memory, external tools beyond the local filesystem, multi-agent patterns, and production deployment to Parts 2 through 5.

## References

- What Is an AI Agent? (AI Agents 101, Part 1) — https://www.aibuilderclub.com/blog/ai-agents-101-part-1
