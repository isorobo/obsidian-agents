---
type: source
status: draft
created: 2026-10-04
title: "smolagents"
authors:
- Hugging Face
organisation: Hugging Face
source_type: repo
venue: GitHub
url: https://github.com/huggingface/smolagents
year: 2024
date_published: 2024-12-05
anthropic: false
topic:
- topic/architectures
- topic/tool-use
tags:
- smolagents
- code-agent
- sandboxing
- react-loop
nlm_id:
nlm_skip: false
watchlist_channel: af-corpus-repos
af_targets:
- af:RSCH-01/smolagents
- af:ADR-0004
- af:RSCH-04/Q14
- af:RSCH-04/Q16
- af:RSCH-04/Q23
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 9f62eaf66592f83ad96b4edec6c575c1a0ad08fa28a2753ba21809daa171997e
---

# smolagents

> Hugging Face, "smolagents", GitHub, 5 December 2024, https://github.com/huggingface/smolagents.

## Summary

smolagents is a barebones Hugging Face library for agents that think in code. The core sits in roughly 1,000 lines in `agents.py`, kept small so users can read and change it. It offers two agent types: CodeAgent, which writes actions as Python snippets, and ToolCallingAgent, which emits JSON tool calls. The README claims code actions cut LLM calls by about 30 percent because one snippet can chain several tool calls. The loop is ReAct style: accumulate memory, generate an action, execute it, store the result, repeat until `final_answer()` is called. Created 5 December 2024, last pushed 30 September 2026, Apache 2.0 (GitHub API, this run). This note covers the README only.

## Key Concepts

- CodeAgent versus ToolCallingAgent: code as the action format versus structured calls.
- Memory as accumulated step history fed back each step.
- Tools can come from MCP servers, LangChain, Hub Spaces or custom code.
- Model-agnostic and modality-agnostic.

## Terminology

- `final_answer()`: the call that ends the loop.
- `LocalPythonExecutor`: in-process executor, stated as not a security boundary.

## Architecture and Implementation

The README lists sandboxing options for untrusted generated code: managed services (E2B, Blaxel, Modal), self-hosted Docker, and the local executor for development only. Agents and tools can be shared through the Hugging Face Hub.

## Code Examples

```python
from smolagents import CodeAgent, WebSearchTool, InferenceClientModel

model = InferenceClientModel()
agent = CodeAgent(tools=[WebSearchTool()], model=model, stream_outputs=True)
agent.run("How many seconds would it take for a leopard at full speed to run through Pont des Arts?")
```

## Best Practices

- Run model-written code in a real sandbox for any production use.
- Prefer code actions when several tool calls compose in one step.

## Warnings and Anti-Patterns

- Treating the local Python executor as isolation.

## Related Concepts

- [[react]]
- [[tool-use]]
- [[the-agent-loop]]
- [[mcp]]

## Future Work

Docs and source on the step loop, managed agents and termination are candidates for part notes.

## References

- https://github.com/huggingface/smolagents
