---
type: glossary
status: draft
created: 2026-07-10
name: Glossary
slug: glossary
topic:
- topic/concepts
tags: [glossary, reference]
synonyms: [terms, definitions]
defined_in: "[[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]"
related_concepts: ["[[what-is-an-ai-agent]]", "[[the-agent-loop]]", "[[best-practices-index]]"]
anthropic: true
---

# Glossary

> Core terms for AI agent engineering, each with a one-line definition and a link to its concept note.

## Terms

- **Agent** — A system that uses a model to direct its own steps toward a goal. See [[what-is-an-ai-agent]].
- **Agent loop** — The cycle of model call, tool call, and observation that drives an agent. See [[the-agent-loop]].
- **Agent vs LLM** — The distinction between a plain model call and a model that acts through tools. See [[agent-vs-llm]].
- **Anti-pattern** — A recurring design that looks helpful yet degrades an agent. See [[anti-patterns-index]].
- **Best practice** — An engineering principle that holds up in production. See [[best-practices-index]].
- **Checkpoint** — A saved state that lets a run resume rather than restart. See [[memory]].
- **Claude Agent SDK** — Anthropic's toolkit for building agents on Claude. See [[claude-agent-sdk]].
- **Claude Code** — Anthropic's terminal coding agent. See [[claude-code]].
- **Context window** — The token budget a model reads at once. See [[memory]].
- **Eval** — A task set that measures agent quality. See [[evaluation]].
- **Guardrail** — A check that screens input or output against policy. See [[evaluation]].
- **MCP** — The Model Context Protocol, an open standard for connecting tools to models. See [[mcp]].
- **Memory** — The state an agent carries across steps and sessions. See [[memory]].
- **Orchestration** — Coordination of models and tools through defined paths. See [[plan-and-execute]].
- **Plan-and-execute** — A pattern that plans the full path, then runs it. See [[plan-and-execute]].
- **Planning** — The step where an agent decomposes a goal into actions. See [[planning-and-reasoning]].
- **Prompt engineering** — The craft of shaping model input for reliable output. See [[prompt-engineering]].
- **RAG** — Retrieval-augmented generation, which grounds output in fetched documents. See [[memory]].
- **ReAct** — A pattern that interleaves reasoning traces with actions. See [[react]].
- **Reflection** — A step where an agent critiques its own output to improve it. See [[reflexion]].
- **Structured output** — A typed, schema-bound response that code can parse. See [[tool-use]].
- **Subagent** — A scoped agent a supervisor delegates a task to. See [[supervisor-worker-multi-agent]].
- **Supervisor** — An agent that assigns work to worker agents. See [[supervisor-worker-multi-agent]].
- **System prompt** — The standing instruction that frames an agent's behaviour. See [[prompt-engineering]].
- **Tool** — A function the model calls to act on the world. See [[tool-use]].
- **Tool use** — The mechanism by which a model invokes a tool. See [[tool-use]].
- **Trajectory** — The full sequence of messages, tool calls, and results in a run. See [[the-agent-loop]].
- **Workflow** — A predefined code path for a well-defined task. See [[workflow-vs-autonomous-agent]].

## Sources

- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]] — https://www.anthropic.com/engineering/building-effective-agents

## See also

- [[MOC - Concepts]]
