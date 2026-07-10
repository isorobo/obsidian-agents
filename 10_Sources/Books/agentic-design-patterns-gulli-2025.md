---
type: source
status: draft
created: 2026-07-10
title: "Agentic Design Patterns: A Hands-On Guide to Intelligent AI Agents"
authors:
- Antonio Gulli
organisation: 
source_type: book
venue: Springer
url: TBD
year: 2025
date_published: 
anthropic: false
topic:
- topic/agent-patterns
- topic/architectures
tags: [prompt-chaining, multi-agent, mcp, rag, guardrails, evaluation]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Agentic Design Patterns: A Hands-On Guide to Intelligent AI Agents

> Full citation: Gulli, A. "Agentic Design Patterns: A Hands-On Guide to Intelligent AI Agents." Springer, 2025.

## Summary

Antonio Gulli's book extracts 21 design patterns for building agentic systems, each covered in a dedicated chapter with a pattern overview, practical applications, a hands-on code example, key takeaways, and references. The chapters run from foundational workflow patterns (prompt chaining, routing, parallelisation, reflection, tool use, planning) through multi-agent collaboration and memory management, into protocol and governance patterns (Model Context Protocol, goal setting, exception handling, human-in-the-loop), knowledge and communication patterns (retrieval-augmented generation, agent-to-agent communication, resource-aware optimisation), and closes with reasoning, guardrails, evaluation, prioritisation, and exploration. The preface frames these as reusable solutions to recurring problems, akin to software design patterns, rather than rigid rules. The book's own copyright page carries no visible year in the extracted front matter; the acknowledgements confirm Springer as publisher, and the PDF file itself carries a creation date of 12 September 2025, so this note treats the edition as a 2025 pre-print pending confirmation of the final publication year.

## Key Concepts

- Twenty-one chapters, each treating one pattern as a self-contained unit with overview, use cases, code, and takeaways.
- Foundational workflow patterns: prompt chaining, routing, parallelisation, reflection, tool use, and planning (Chapters 1 to 6).
- Collaboration and memory patterns: multi-agent collaboration, memory management, and learning and adaptation (Chapters 7 to 9).
- Protocol and control patterns: Model Context Protocol, goal setting and monitoring, exception handling and recovery, and human-in-the-loop (Chapters 10 to 13).
- Knowledge and communication patterns: retrieval-augmented generation, agent-to-agent communication, and resource-aware optimisation (Chapters 14 to 16).
- Advanced and production patterns: reasoning techniques, guardrails and safety, evaluation and monitoring, prioritisation, and exploration and discovery (Chapters 17 to 21).
- The preface's "agentic canvas" metaphor treats frameworks as the infrastructure on which patterns run, distinct from the patterns themselves.

## Terminology

- **Agentic system** — a computational entity that perceives its environment, decides on goals, and executes actions autonomously, as distinct from a rigid, script-following program.
- **Agentic canvas** — the book's metaphor for the underlying infrastructure and frameworks that host an agent's state, tool access, and control flow.
- **Level 0 to Level 3 agents** — the book's complexity ladder, from a bare reasoning engine with no tools, through tool-connected and strategic problem-solvers, to collaborative multi-agent systems.
- **Context engineering** — the discipline of selecting, packaging, and managing the most relevant information for each step an agent takes.

## Architecture and Implementation

Each chapter pairs a pattern description with a runnable implementation, so the book doubles as an architecture reference and an implementation cookbook. The five-step agent loop the preface describes (receive goal, gather context, plan, act, learn) recurs across chapters as the shared skeleton that each pattern extends or specialises. Chapters on the Model Context Protocol, agent-to-agent communication, and multi-agent collaboration treat coordination and interoperability as first-class architectural concerns, not afterthoughts layered onto a single-agent design.

## Code Examples

The book ships hands-on code in three frameworks: LangChain, together with its stateful extension LangGraph, for chaining and graph-based agent flows; CrewAI for orchestrating multiple agents, roles, and tasks; and Google's Agent Developer Kit (Google ADK) for building, evaluating, and deploying agents on Google's AI infrastructure. Most chapters carry at least one runnable example per framework, so a reader can compare how the same pattern looks across the three canvases.

## Best Practices

- Treat patterns as reusable templates for recurring problems, not fixed rules to follow without judgement.
- Prepare clean data, consistent metadata, and well-defined APIs before layering agents onto existing systems, per the foreword's warning against messy systems plus agents.
- Curate context deliberately at each step rather than passing an agent's full working state forward unchanged.
- Run and adapt the accompanying code examples rather than reading the pattern description alone.

## Warnings and Anti-Patterns

The foreword by Marco Argenti, CIO of Goldman Sachs, warns that messy, inconsistent systems combined with agents produce confident, plausible garbage rather than useful output. It draws a sharp line between low-stakes agent errors, such as a flawed recipe suggestion, and high-stakes errors in domains such as trading, risk management, or client data handling, where the same failure mode carries real cost. The book positions guardrails and evaluation (Chapters 18 and 19) as the patterns that address this risk directly, rather than treating safety as a separate concern from the core design patterns.

## Related Concepts

- [[the-agent-loop]]
- [[tool-use]]
- [[memory]]
- [[planning-and-reasoning]]
- [[mcp]]
- [[evaluation]]
- [[40_Guides/agentic-design-patterns-plain-english|Agentic Design Patterns — Plain English Guide]]

## Future Work

The preface's "Future of Agents" section sets out five hypotheses beyond the 21 patterns: the emergence of generalist agents alongside small, composable specialist agents; deep personalisation and proactive goal discovery; embodiment and physical-world interaction; an agent-driven economy of autonomous economic participants; and goal-driven, metamorphic multi-agent systems that restructure their own topology. These sit outside the pattern chapters as directional hypotheses rather than documented patterns.

## References

- Cloudera, Inc. (April 2025). "96% of enterprises are increasing their use of AI agents." https://www.cloudera.com/about/news-and-blogs/press-releases/2025-04-16-96-percent-of-enterprises-are-expanding-use-of-ai-agents-according-to-latest-data-from-cloudera.html
- Deloitte. "Autonomous generative AI agents: still under development." https://www.deloitte.com/us/en/insights/industry/technology/technology-media-and-telecom-predictions/2025/autonomous-generative-ai-agents-still-under-development.html
- Market.us. "Global Agentic AI Market Size, Trends and Forecast 2025-2034." https://market.us/report/agentic-ai-market/
