---
type: concept
status: draft
created: 2026-07-10
name: Memory
slug: memory
topic:
- topic/memory
- topic/foundations
tags:
- memory
- context
- state
synonyms:
- agent memory
- episodic memory
- long-term memory
defined_in: "[[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]"
related_concepts:
- "[[what-is-an-ai-agent]]"
- "[[agent-vs-llm]]"
- "[[the-agent-loop]]"
---

# Memory

> Memory is the store that lets an agent carry information across turns and sessions beyond the fixed context window.

## Summary

A language model forgets past its context window. Memory removes that limit. An agent writes facts, results, and reflections to a store outside the prompt. It reads the relevant parts back when a task needs them. Anthropic lists memory as one of the three augmentations of the base model, beside retrieval and tools. MemGPT frames the problem as virtual context management, borrowed from operating systems. Memory turns a stateless call into a system that learns across time.

## Key Concepts

- The context window bounds what a single call can hold.
- Memory stores state outside the prompt and reads it back on demand.
- Short-term memory holds the current task; long-term memory spans sessions.
- Episodic reflection lets an agent learn from past trials.

## Detail

Memory splits by horizon. Short-term memory lives in the context window and holds the running task. Long-term memory lives in an external store, such as a file, a vector index, or a database. The agent writes to the store and retrieves the parts a step needs. This split lets an agent exceed the window without losing the thread.

MemGPT models the store as tiers, like an operating system paging between memory and disk. The agent moves data between the window and the store as the task demands. Reflexion adds a second use. An agent writes verbal reflections on past failures to an episodic buffer. It reads those reflections on the next trial and improves its decisions.

## Trade-offs and Limits

Memory lets an agent hold long tasks and learn across sessions. It also adds retrieval cost, staleness, and a chance of poisoned or wrong recall. A crowded memory buries the signal the task needs. Curated writes and sharp retrieval keep memory an asset rather than noise.

## Related

- [[what-is-an-ai-agent]]
- [[agent-vs-llm]]
- [[the-agent-loop]]
- [[reflexion]]

## Sources

- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]
- MemGPT: Towards LLMs as Operating Systems — https://arxiv.org/abs/2310.08560
- Reflexion: Language Agents with Verbal Reinforcement Learning — https://arxiv.org/abs/2303.11366

## See also

- [[MOC - Memory]]
