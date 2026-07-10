---
type: concept
status: draft
created: 2026-07-10
name: Prompt Engineering
slug: prompt-engineering
topic:
- topic/prompt-engineering
- topic/foundations
tags: [prompt-engineering, prompting, xml-tags, examples, chain-of-thought, system-prompt]
synonyms: [Prompt Engineering, Prompting]
defined_in: "[[10_Sources/Docs/claude-agent-sdk-overview|Agent SDK overview]]"
related_concepts: ["[[tool-use]]", "[[claude-code]]", "[[best-practices-index]]"]
anthropic: true
---

# Prompt Engineering

> Prompt engineering shapes the instructions to a model to meet defined success criteria through structure, examples, and technique.

## Summary

Prompt engineering improves a model output through the prompt alone. Anthropic frames it as the step after success criteria and evaluations exist. A first draft prompt gives the baseline. Techniques then raise quality against the criteria. Not every failure suits a prompt fix; latency and cost often favour a different model.

## Key Concepts

- Be clear and direct; state the task and the format.
- Use examples, also called multishot prompting.
- Give Claude room to think through chain-of-thought reasoning.

## Detail

Anthropic groups the core techniques into a short list. Clarity comes first: name the task, the audience, and the output shape. Examples show the model the target form. Chain-of-thought reasoning improves multi-step work. XML tags structure a prompt and separate a document from an instruction. A system prompt sets a role. A prefill steers the start of the response. Prompt chaining splits a complex task into linked steps. A query placed after long documents can raise response quality on multi-document inputs. The Claude Console adds a prompt generator, templates, and a prompt improver.

## Trade-offs and Limits

Prompt engineering costs little and iterates fast. It controls tone, format, and reasoning depth. It cannot add knowledge the model lacks or cut token cost on its own. A model swap or a retrieval step solves problems a prompt cannot. Context engineering extends the idea to what fills the whole context window.

## Related

- [[tool-use]]
- [[claude-code]]
- [[best-practices-index]]

## Sources

- https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview
- https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

## See also

- [[MOC - Prompt Engineering]]
