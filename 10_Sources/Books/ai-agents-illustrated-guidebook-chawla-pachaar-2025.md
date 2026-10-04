---
type: source
status: draft
created: 2026-08-13
title: "AI Agents: The Illustrated Guidebook"
authors:
- Avi Chawla
- Akshay Pachaar
organisation: "Daily Dose of Data Science"
source_type: book
venue: "Daily Dose of Data Science, 2025 Edition"
url: TBD
year: 2025
date_published: 2025
anthropic: false
topic:
- topic/foundations
- topic/concepts
tags: [ai-agents, illustrated-guide, crewai, agent-design-patterns, agentic-levels]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
af_targets:
- af:ADR-0001
- af:RSCH-04/Q01
- af:RSCH-04/Q02
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 3bc5b6be386222e12b850e4f160c664c280b8a0bcb7c24797e47a388bf1a64dc
---

# AI Agents: The Illustrated Guidebook

> Full citation: Chawla, A. and Pachaar, A. "AI Agents: The Illustrated Guidebook", 2025 Edition. Daily Dose of Data Science, 2025.

## Summary

This 117-page illustrated guide from Daily Dose of Data Science teaches agent
construction in two sections. Section one defines an AI agent, separates it
from an LLM and from RAG, and sets out six building blocks: role-playing,
focus, tools, cooperation, guardrails, and memory. It then presents five
agentic design patterns and five levels of agentic AI systems. Section two
walks through 12 build projects, from agentic RAG to a multi-agent book
writer. CrewAI carries most of the code, with Ollama serving local models such
as DeepSeek-R1 and Qwen 3. The authors state a reading time of about 8 hours
and open with a two-minute assessment that routes each reader to the relevant
chapters. This volume differs in scope from its sibling,
[[10_Sources/Books/mcp-illustrated-guidebook-chawla-pachaar-2025|MCP: The Illustrated Guidebook]]:
the sibling covers one protocol and its host-client-server architecture, while
this volume covers how an agent is composed, patterned, and staged, and treats
MCP as one way to supply a tool.

## Key Concepts

- An agent is an autonomous system that reasons, plans, finds sources, acts,
  and corrects itself.
- The book separates three layers: the LLM is the brain, RAG feeds the brain
  fresh information, and the agent decides and acts.
- Six building blocks make an agent reliable: role-playing, focus, tools,
  cooperation, guardrails, and memory.
- Five design patterns cover the field: reflection, tool use, ReAct, planning,
  and multi-agent.
- Five levels grade agency: basic responder, router, tool calling,
  multi-agent, and autonomous.
- Agency rises as the LLM takes more control over program flow.
- A narrow role and a narrow task beat one agent that does everything.

## Terminology

- **Role-playing**: assigning a clear, specific role to shape the agent's
  reasoning and retrieval.
- **Focus**: restricting an agent to one narrow task to cut hallucination.
- **Guardrails**: limits that stop an agent looping, overusing a tool, or
  making a bad call.
- **Short-term memory**: state that exists during one execution, such as
  recent conversation history.
- **Long-term memory**: state that persists after execution, such as user
  preferences across interactions.
- **Entity memory**: stored information about key subjects under discussion,
  such as customer details.
- **Reflection pattern**: the model reviews its own work and iterates until it
  produces a final response.
- **ReAct pattern**: a loop of thought, action, and observation that repeats
  until the agent reaches an answer.
- **Planning pattern**: the model builds a roadmap first by subdividing tasks
  and outlining objectives.
- **Router pattern**: the LLM makes a basic decision on which function or path
  to take.
- **Autonomous pattern**: the LLM generates and executes new code on its own.
- **Crew**: the CrewAI unit that binds agents, tasks, and execution together.
- **Flow**: the CrewAI construct that sequences crews into a larger pipeline.

## Architecture and Implementation

The guide builds an agent from six blocks. A role fixes how the agent reasons
and what it retrieves. Focus keeps one agent on one narrow task, since
overloading produces confusion and poor output. Tools give the agent web
search, API and database access, code execution, and document analysis.
Cooperation splits work across specialised agents that exchange feedback: one
gathers data, one assesses risk, one builds strategy, and one writes the
report. Guardrails cap tool usage and supply a fallback when an agent fails.
Memory carries context across turns and across sessions in three forms.

The five patterns compose rather than compete. Reflection adds
self-evaluation. Tool use adds outside information. ReAct combines the two in
a thought, action, and observation loop, which the authors name as the CrewAI
default. Planning subdivides a task before execution; the guide notes that
CrewAI turns this on with `planning=True`. The multi-agent pattern gives each
agent its own tools and lets agents hand work to each other.

The five levels of agentic AI systems grade how much control the model holds
over program flow. A basic responder takes input and returns output with
little control. A router picks a path. At tool calling, the model decides when
to call a tool and what arguments to pass. In the multi-agent level, a manager
agent coordinates sub-agents and decides the next step; a human sets the
hierarchy, the roles, and the tools. At the autonomous level, the model writes
and runs new code, acting as an independent developer.

The project chapters apply this stack. A retriever agent and a writer agent
form the agentic RAG system, deployed behind LitServe. Two crews, an outline
crew and parallel writer crews, produce the book writer. A planning crew and a
documentation crew produce the documentation writer. Zep supplies the memory
layer for the human-like memory project, which visualises a user's
conversations as a knowledge graph.

## Code Examples

The extract captures the surrounding prose more than the code blocks, which
sit in images. Four fragments remain legible. A custom CrewAI tool subclasses
`BaseTool` and implements a `_run` method that the agent calls; the worked
example is a `CurrencyConverterTool` that fetches live exchange rates from an
external API and handles a failed request or an invalid currency code. The
same tool is then re-exposed through a `server.py` script as an MCP tool,
`convert_currency`, served at `http://localhost:8081/sse`, and consumed by a
CrewAI agent through `MCPServerAdapter`. The agentic RAG deployment implements
three LitServe methods that run in order: `decode_request`, then `predict`,
then `encode_request`. Several agents return Pydantic models to guarantee
structured output for the next stage.

## Best Practices

- Give each agent a clear, specific role before tuning anything else.
- Keep one agent on one narrow task, and add agents rather than tasks.
- Add a tool only where the task needs it.
- Split work across specialised agents that exchange feedback.
- Cap tool usage and define a fallback where an agent or a human takes over.
- Match the memory type to the need: short-term, long-term, or entity.
- Return structured output through Pydantic where one stage feeds the next.
- Execute generated code inside a sandbox, as the CrewAI code interpreter tool
  does.
- Expose a reusable tool through an MCP server once, then share it across
  crews and flows.

## Warnings and Anti-Patterns

- Overloading one agent with tasks or data produces confusion, inconsistency,
  and poor results.
- More tools do not mean better results; an unrelated tool degrades the agent.
- Letting the model guess a value it could fetch, such as an exchange rate,
  invites error.
- Embedding the same tool in every crew duplicates work that one MCP server
  removes.
- Deploying an agent without memory makes every interaction a blank slate.
- An agent without guardrails hallucinates, loops without end, or makes bad
  calls.
- A domain agent that reads stale sources, such as a legal assistant citing
  outdated law, states false claims.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[agent-vs-llm]]
- [[the-agent-loop]]
- [[react]]
- [[reflexion]]
- [[plan-and-execute]]
- [[tool-use]]
- [[memory]]
- [[supervisor-worker-multi-agent]]
- [[workflow-vs-autonomous-agent]]
- [[retrieval-augmented-generation]]
- [[agent-patterns-index]]
- [[mcp]]

Sibling and comparison sources:

- [[10_Sources/Books/mcp-illustrated-guidebook-chawla-pachaar-2025|MCP: The Illustrated Guidebook]], the same authors on the protocol layer this book treats as one tool option.
- [[10_Sources/Books/agentic-design-patterns-gulli-2025|Agentic Design Patterns]], a longer treatment of the same pattern catalogue.
- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]], which draws the workflow and agent line this book grades as five levels.

## Future Work

The book flags no open problem and proposes no research agenda. It closes on
the twelfth project with no concluding chapter. Each project chapter ends with
a link to the full code, and those links arrive garbled in the extract, so the
code-level detail behind the 12 projects stays outside this note.

## References

- Publisher: Daily Dose of Data Science, DailyDoseofDS.com.
- The book opens with a two-minute self-assessment that recommends chapters;
  the printed short link is unreadable in the extract.
- Per-project code links point to dailydoseofds.com articles and to the
  authors' ai-engineering-hub GitHub repository.
