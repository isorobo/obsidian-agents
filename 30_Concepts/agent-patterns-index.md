---
type: concept
status: draft
created: 2026-07-12
name: Agent Patterns Index
slug: agent-patterns-index
topic:
- topic/agent-patterns
tags: [index, design-patterns]
synonyms: [agent design patterns, agentic patterns]
defined_in: "[[10_Sources/Books/agentic-design-patterns-gulli-2025|Agentic Design Patterns (Gulli)]]"
related_concepts: ["[[react]]", "[[workflow-vs-autonomous-agent]]", "[[the-agent-loop]]"]
anthropic: false
af_targets:
- af:ADR-0007
- af:DELEG-03
- af:RSCH-04/Q30
- af:RSCH-04/Q31
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 7f5448f2fee325ef3bb62cccaf86c6d251ce47ce51cfee0e8f54a8125989dd62
---

# Agent Patterns Index

> The single lookup target for Gulli's 21 agent design patterns, each with a trigger and a trade-off.

## Summary

This note consolidates the six-source `topic/agent-patterns` cluster into one lookup target. Antonio Gulli's 21 patterns form the spine. Each entry names the pattern, states its trigger condition, and states its trade-off, so a later citation quotes an independent passage per pattern. Two entries link out to a dedicated concept note for depth; the rest resolve here. This note is the sole carrier of `topic/agent-patterns`, so the MOC dataview query returns exactly one note.

## Patterns

- **Prompt Chaining** — decompose a complex task into a sequence of single-objective steps, with gates that validate schema and confidence between steps (name matches Anthropic). Trigger: one prompt juggles several objectives and accuracy drops. Trade-off: buys accuracy with added latency.
- **Routing** — classify input and direct it to a specialised handler, from cheap rule-based to accurate LLM-based architectures (name matches Anthropic). Trigger: heterogeneous input types each need different handling. Trade-off: buys specialisation with a misclassification risk at the routing step.
- **Parallelisation** — run independent sub-tasks concurrently through Fan-Out/Fan-In, Sectioning, or Voting (name matches Anthropic). Trigger: sub-tasks are independent and latency matters. Trade-off: buys speed and coverage with duplicated token spend.
- **Reflection** — the agent critiques its own output and revises across Self-Reflection, Evaluator-Optimiser, and Debate architectures. Anthropic names the generator-plus-evaluator flavour Evaluator-Optimiser. Trigger: first-pass output needs quality one shot cannot reach. Trade-off: buys quality with extra token spend and latency.
- **Tool Use** — the model emits structured function calls a runtime executes against external systems, where interface quality drives accuracy. Trigger: the task needs data or actions beyond the model's own parameters. Trade-off: buys reach with tool-design and failure-handling cost.
- **Planning** — decompose a goal into sub-tasks before acting, via ReAct, Plan-and-Execute, or Tree of Thoughts. Trigger: a multi-stage goal resists a single forward pass. Trade-off: buys structure with planning overhead and replanning cost. See [[react]] for depth on the interleaved-reasoning strategy.
- **Multi-Agent Collaboration** — distribute work across specialist agents through Orchestrator-Workers, Manager, or Decentralised/Handoff coordination. Anthropic names the lead-delegates-to-workers coordination Orchestrator-Workers. Trigger: one agent's system prompt overloads or it keeps selecting the wrong tool. Trade-off: buys parallel specialisation with coordination and token cost.
- **Memory Management** — a five-tier architecture spanning working, episodic, semantic, procedural, and meta-memory. Trigger: the task spans more context than one window holds. Trade-off: buys continuity with retrieval complexity and stale-memory risk. Gulli's tiers sort memory by kind; see [[memory]] for the horizon split that sorts the same store by how long a fact survives.
- **Learning and Adaptation** — generate, critique, store an insight, and retry, scaling from Reflexion to the ACE loop's persistent playbook. Trigger: repeated runs make the same avoidable mistake. Trade-off: buys improvement with storage and curation overhead.
- **Model Context Protocol (MCP)** — a universal client-server standard separating read-only Resources from executable Tools with on-demand discovery. Trigger: agent-tool integration sprawls across bespoke connectors. Trade-off: buys interoperability with protocol and server-maintenance cost.
- **Goal Setting and Monitoring** — compare each action's environmental result against the objective, with explicit stopping conditions. Trigger: an open loop risks running past its goal. Trade-off: buys control with monitoring overhead and added state.
- **Exception Handling and Recovery** — a fallback chain of primary handler, fallback handler, and response agent, driven by error classification. Trigger: external calls fail transiently or permanently in production. Trade-off: buys resilience with fallback-path complexity.
- **Human-in-the-Loop** — three oversight tiers (HITL, HOTL, HIC) placed on a reversibility framework. Trigger: an irreversible or high-stakes action needs approval. Trade-off: buys safety with human latency and throughput cost.
- **Knowledge Retrieval (RAG)** — retrieve documents, augment the prompt, and ground the response in evidence rather than training data (Gulli's prose calls this retrieval-augmented generation). Trigger: the answer needs facts the model was never trained on. Trade-off: buys grounding with retrieval and re-ranking cost.
- **Inter-Agent Communication (A2A)** — an open HTTP protocol letting agents on different frameworks discover and delegate through a published Agent Card (Gulli's prose calls this agent-to-agent communication). Trigger: agents on separate stacks must interoperate. Trade-off: buys cross-framework reach with protocol and trust-boundary cost.
- **Resource-Aware Optimisation** — match token spend, latency, and compute to task need through model routing, context efficiency, and caching. Trigger: cost or latency exceeds the task's value. Trade-off: buys efficiency with routing complexity and tuning effort. See [[workflow-vs-autonomous-agent]] for depth on the agents-versus-workflows distinction.
- **Reasoning Techniques** — Chain of Thought and Extended Thinking expose the model's reasoning, with an effort parameter matching depth to demand. Trigger: a hard problem needs visible, staged reasoning. Trade-off: buys reasoning depth with token spend and latency.
- **Guardrails and Safety Patterns** — defence in depth against prompt injection, memory poisoning, and self-replicating attacks. Trigger: untrusted input or tools reach the agent. Trade-off: buys safety with added checks and engineering cost.
- **Evaluation and Monitoring** — LLM-as-Judge scores output against a rubric while trajectory evaluation measures action validity and plan adherence. Trigger: regressions ship undetected without a measured baseline. Trade-off: buys confidence with eval-authoring and run cost.
- **Prioritisation** — an urgency-importance matrix orders competing demands, with dynamic re-prioritisation as conditions change. Trigger: competing tasks exceed the available budget. Trade-off: buys focus with scheduling overhead and re-ordering churn.
- **Exploration and Discovery** — curiosity-driven queries and hypothesis-testing loops generate knowledge the agent was not asked for. Trigger: the task rewards finding unknown unknowns. Trade-off: buys discovery with a bounded exploration budget, near 10% of token spend.

## Detail

The plain-English guide groups the 21 into four parts: seven foundational workflow patterns (1 to 7), four cognitive-infrastructure patterns (8 to 11), three resilience-and-knowledge patterns (12 to 14), and seven advanced production patterns (15 to 21). The Gulli source note groups the same 21 into five chapter-clusters. Both totals match; the guide names are canonical here. No production system runs one pattern alone. Gulli's closing chapter composes them into four reference architectures: a customer service agent, a research agent, a coding agent, and an enterprise workflow agent.

## Execution substrates

Patterns are design-time choices. A substrate is where the pattern runs. Claude Code dynamic workflows are the native substrate when code holds the control.

| MindStudio pattern | Vault entry | Workflow-substrate fit |
|---|---|---|
| Sequential Flow | **Prompt Chaining** | Strong — script holds the step sequence |
| Operator | **Multi-Agent Collaboration** (Orchestrator-Workers) | Strong — script is the orchestrator |
| Split-and-Merge | **Parallelisation** | Strong — pipeline/parallel primitives |
| Agent Teams | **Multi-Agent Collaboration** | Partial — peer sessions suit agent teams; workflows suit fan-out |
| Headless | **Goal Setting and Monitoring** + autonomous loop | Conditional — validated-in-interactive-mode first |

A workflow cannot pause for user input, so Human-in-the-Loop and interactive intake stay outside the script.

## Related

- [[react]]
- [[workflow-vs-autonomous-agent]]
- [[the-agent-loop]]

## Sources

- [[10_Sources/Books/agentic-design-patterns-gulli-2025|Agentic Design Patterns (Gulli)]]
- [[40_Guides/agentic-design-patterns-plain-english|Agentic Design Patterns — Plain English Guide]]
- [[10_Sources/Docs/claude-code-dynamic-workflows|Claude Code dynamic workflows]]
- [[10_Sources/Blog/mindstudio-claude-code-5-workflow-patterns|MindStudio — 5 workflow patterns]]

## See also

- [[MOC - Agent Patterns]]
