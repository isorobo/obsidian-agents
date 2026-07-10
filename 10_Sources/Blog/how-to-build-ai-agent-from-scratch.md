---
type: source
status: draft
created: 2026-07-11
title: "How to Build an AI Agent from Scratch in Python (2026)"
authors:
- AI Builder Club
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 2.1
url: https://www.aibuilderclub.com/blog/how-to-build-ai-agent-from-scratch
year: 2026
date_published: 2026-05-07
anthropic: false
topic:
- topic/foundations
tags:
- agent-loop
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
---

# How to Build an AI Agent from Scratch in Python (2026)

> AI Builder Club, "How to Build an AI Agent from Scratch in Python (2026)", Build AI Agents Course, 7 May 2026, https://www.aibuilderclub.com/blog/how-to-build-ai-agent-from-scratch.

## Summary

Chapter 2 opens by rebuilding the Chapter 1 agent as a self-contained, seven-step exercise: an agent reduces to three primitives — an LLM that supports tool use, a set of Python functions as tools, and a loop tying the two together — with memory, planning, and reflection treated as later additions on top of that base, not separate primitives. The lesson argues that most production agents at the companies the authors work with run on hand-written loops rather than frameworks, and that understanding the loop directly teaches more than adopting a framework first.

## Key Concepts

- An agent is three primitives: a tool-capable LLM, a tool registry, and a loop; everything else (memory, planning, reflection) sits on top.
- Tool descriptions function as the model's only source of truth about what a tool does; vague or misleading descriptions cause tool-selection errors before any code runs.
- A step cap (roughly 10 to 25) is not optional — it is what prevents a vague goal from turning into a runaway, expensive loop.
- Custom code versus a framework (the article compares against LangChain's `AgentExecutor`) trades understanding against convenience; the lesson does not declare a universal winner.

## Terminology

- Tool registry — a mapping from tool names to their Python implementations, checked against the model's requested tool name at execution time.
- `stop_reason` — the signal an API response carries indicating whether the model finished (`end_turn`) or wants a tool executed (`tool_use`); an agent that ignores other stop reasons (such as hitting `max_tokens`) fails silently.

## Architecture and Implementation

The reference build runs in seven steps: install the SDK, define two starter tools (`list_files`, `read_file`), describe them to the model as JSON Schema with factual, specific descriptions, implement the roughly 35-line loop (send messages and tool definitions, check `stop_reason`, execute requested tools, append results, repeat to `end_turn` or the step cap), run it against a real directory, add error handling that returns failures to the model as strings rather than raising, and add a system prompt to specialise the agent's behaviour. The lesson treats the system prompt as carrying outsized weight: it sets purpose, constraints, and tone in one place.

## Code Examples

A complete, runnable 60-line agent using the Anthropic SDK, plus a companion tool registry and a system-prompt example ("You are a code analysis agent").

## Best Practices

- Always append the assistant's response to message history; skipping this step erases the model's memory of its own prior turn.
- Serialise every tool result to a string or JSON before returning it to the model.
- Cap steps explicitly; do not rely on the model to self-terminate.
- Keep the initial goal specific; vague goals drive excessive, unnecessary tool calls.
- Start with two or three tools before adding more.

## Warnings and Anti-Patterns

- Misleading tool descriptions confuse the model's selection logic in ways that are hard to debug after the fact.
- Ignoring non-`end_turn` stop reasons, such as `max_tokens`, causes silent truncation that looks like a completed task.
- Treating the framework-versus-custom-code question as settled in either direction misses that the trade-off is understanding against convenience, not correctness against incorrectness.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[the-agent-loop]]
- [[tool-use]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson's own "what to build next" section points directly at 2.2 (multi-agent coordination), memory systems, and real tools beyond the local filesystem — the same three directions Chapter 1 deferred.

## References

- How to Build an AI Agent from Scratch in Python (2026) — https://www.aibuilderclub.com/blog/how-to-build-ai-agent-from-scratch
