---
type: source
status: draft
created: 2026-07-10
title: "The Landscape of Emerging AI Agent Architectures for Reasoning, Planning, and Tool Calling: A Survey"
authors:
- Tula Masterman
- Sandi Besen
- Mason Sawtell
- Alex Chao
organisation: 
source_type: paper
venue: 
url: https://arxiv.org/abs/2404.11584
year: 2024
date_published: 2024-04-17
anthropic: false
topic:
- topic/architectures
- topic/research-papers
tags: [survey, taxonomy, react, reflexion, multi-agent]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# The Landscape of Emerging AI Agent Architectures for Reasoning, Planning, and Tool Calling: A Survey

> Full citation: Masterman, Besen, Sawtell, Chao. "The Landscape of Emerging AI Agent Architectures for Reasoning, Planning, and Tool Calling: A Survey." arXiv:2404.11584, 2024. https://arxiv.org/abs/2404.11584

## Summary

This survey maps the post-ChatGPT shift from chat-over-documents retrieval augmented generation towards autonomous, orchestrated agent systems. It defines an AI agent as a language model-powered entity that plans and takes actions to execute a goal, and it sorts implementations into single-agent and multi-agent architectures. Each agent carries a persona that states its role and the tools it can call, a design choice the survey treats as essential to task execution. The paper builds a taxonomy across these architectures, reviews reasoning and planning approaches, and examines tool calling as the mechanism that lets an agent break a large problem into smaller, solvable steps. It closes on the limits of current evaluation methodology and the open questions that remain for the field.

## Key Concepts

- An AI agent is a language model-powered entity that plans and acts to reach a goal.
- Architectures split into single-agent and multi-agent designs.
- A persona defines an agent's role and the tools available to it.
- Planning commonly follows one of five major approaches, including task decomposition and memory-augmented planning.
- Tool calling lets an agent decompose a complex problem into manageable subproblems.
- Multi-agent systems often call tools in parallel across agents to raise throughput.

## Terminology

- **Agent persona** — the description of an agent's role and available tools, set before task execution begins.
- **Task decomposition** — a planning approach that splits a complex goal into smaller subtasks.
- **Memory-augmented planning** — a planning approach that draws on stored past experience to guide the next action.
- **Self-correction** — an agent's capacity to revise its own output after detecting an error, central to ReAct and RAISE.

## Architecture and Implementation

The survey groups agent architectures into two families and evaluates each against reasoning strength, planning approach, and tool-calling design.

**Single-agent architectures** favour reasoning before action. ReAct interleaves reasoning traces with actions in a single loop, so the agent states its intent, acts, and observes the result before its next step. See [[react]]. RAISE extends this pattern with an explicit memory mechanism, allowing the agent to draw on prior scratchpad state rather than reason from a blank slate on each step. Reflexion adds a further self-correction layer: the agent writes a verbal reflection after a failed trial and reads that reflection back on the next attempt, improving its decisions without weight updates. See [[reflexion]].

**Multi-agent architectures** trade a single reasoning loop for a team of agents with distinct personas and dynamic role assignment. Embodied LLM Agents apply this pattern to physical or simulated environments, where agents must ground plans in perception and action feedback rather than text alone. DyLAN builds a dynamic team structure, forming and reconfiguring agent teams per task rather than fixing roles in advance. AgentVerse organises multi-agent collaboration through defined stages, moving a task through expert recruitment, decision-making, action execution, and evaluation. These frameworks depend on the coordination pattern discussed in [[supervisor-worker-multi-agent]], where one agent directs subordinate agents and integrates their output.

The survey frames the choice between single-agent and multi-agent designs as a trade-off. A single agent keeps state and control simple but bounds throughput to one reasoning loop. A multi-agent team parallelises tool calling and specialises personas per subtask, at the cost of coordination overhead and harder evaluation. Both families depend on the reasoning and planning capacity discussed in [[planning-and-reasoning]] and both execute within the observe-act-reflect structure set out in [[the-agent-loop]].

## Code Examples

Not applicable. The survey is architectural and does not publish reference implementations.

## Best Practices

- Match architecture to task shape: a single well-scoped task favours a single agent with a tight reasoning loop; a task that decomposes into independent subtasks favours a multi-agent team.
- Give every agent an explicit persona that states its role and its available tools before execution starts.
- Pair a planning approach with a memory mechanism where a task spans multiple steps, so the agent can draw on prior state rather than re-derive it.
- Add self-correction, such as Reflexion's verbal reflection step, where failure recovery matters more than raw speed.

## Warnings and Anti-Patterns

- The survey flags inconsistent benchmarks across agent evaluations, which makes cross-paper comparison unreliable.
- Scalability issues appear as team size grows in multi-agent systems, since coordination cost rises with agent count.
- The paper calls out unaddressed bias in agent decision-making as an open risk, not a solved problem.
- Real-world applicability remains limited where evaluation relies on narrow, synthetic benchmarks rather than production conditions.

## Related Concepts

- [[react]]
- [[reflexion]]
- [[supervisor-worker-multi-agent]]
- [[planning-and-reasoning]]
- [[the-agent-loop]]
- [[tool-use]]
- [[agent-vs-llm]]
- [[what-is-an-ai-agent]]

## Future Work

The authors identify evaluation methodology as the field's main gap: benchmarks remain inconsistent across papers, which blocks reliable comparison between architectures. They call for research into scalability as agent teams grow, for methods that address bias in agent decision-making, and for evaluation designs that better reflect real-world applicability rather than narrow synthetic tasks.

## References

- Masterman, T., Besen, S., Sawtell, M., Chao, A. "The Landscape of Emerging AI Agent Architectures for Reasoning, Planning, and Tool Calling: A Survey." arXiv:2404.11584, 2024. https://arxiv.org/abs/2404.11584
