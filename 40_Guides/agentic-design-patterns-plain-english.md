---
type: guide
status: draft
created: 2026-07-10
name: Agentic Design Patterns — Plain English Guide
slug: agentic-design-patterns-plain-english
topic:
- topic/agent-patterns
tags: [design-patterns, plain-english, gulli]
synonyms: []
related_concepts:
- "[[the-agent-loop]]"
- "[[tool-use]]"
- "[[memory]]"
- "[[supervisor-worker-multi-agent]]"
- "[[mcp]]"
---

# Agentic Design Patterns — Plain English Guide

> A plain-English map of Antonio Gulli's 21 agent design patterns, grouped into four parts, stripped of framework code.

## Goal

This guide gives the reader a durable, framework-agnostic mental map of the 21
patterns in Gulli's *Agentic Design Patterns*. Gulli separates the canvas from
the painting. The canvas is the framework: LangGraph, CrewAI, Google ADK,
Claude Agent SDK. The painting is the pattern: Prompt Chaining, Routing,
Reflection, Memory. A pattern learned on one canvas transfers to the next. The
canvas changes; the pattern stays. This guide teaches the painting, not the
canvas.

## Prerequisites

- Familiarity with [[what-is-an-ai-agent]].
- Familiarity with [[the-agent-loop]], the perceive-reason-act-observe cycle
  that Gulli calls the five-step agentic loop: get the mission, scan the
  scene, think it through, take action, learn and get better.

## Steps

Read the four parts in order. Parts One and Two build sequentially. Parts
Three and Four can follow in either order, though Guardrails (18) and
Evaluation (19) form a natural pair.

### Part One: Foundational Workflow Patterns

Seven patterns cover execution structure: sequencing, routing, concurrency,
self-evaluation, tool integration, planning, and collaboration.

1. **Prompt Chaining** — decompose a complex task into a sequence of
   single-objective steps. Gates between steps validate schema and confidence
   before data passes downstream. Trades latency for accuracy.
2. **Routing** — classify input and direct it to a specialised handler. Five
   architectures: rule-based, semantic, hierarchical, auction-based, and
   LLM-based, ranging from cheap and brittle to expensive and accurate.
3. **Parallelisation** — run independent sub-tasks concurrently. Fan-Out/Fan-In
   distributes one input to many processors; Sectioning splits a dataset
   across processors; Voting runs the same prompt many times and takes the
   majority.
4. **Reflection** — the agent critiques its own output and revises. Three
   architectures: Self-Reflection (one agent), Evaluator-Optimizer (generator
   plus separate evaluator), and Debate (multiple agents argue, a judge
   decides).
5. **Tool Use** — the model generates structured function calls that a
   runtime executes against external systems. Tool design quality, the
   Agent-Computer Interface, determines accuracy as much as model choice.
6. **Planning** — decompose a goal into sub-tasks before acting. Three
   strategies: ReAct (interleave reasoning and action), Plan-and-Execute
   (global plan upfront), and Tree of Thoughts (explore multiple branches and
   prune).
7. **Multi-Agent Collaboration** — distribute work across specialist agents.
   Three coordination patterns: Orchestrator-Workers (lead delegates to
   workers), Manager (central agent treats sub-agents as tools), and
   Decentralized/Handoff (peers transfer control directly).

### Part Two: Cognitive Infrastructure

Four patterns cover what an agent remembers, how it improves, how it connects
to systems, and how it tracks progress.

8. **Memory Management** — a five-tier architecture: working (context
   window), episodic (past interactions), semantic (domain knowledge),
   procedural (workflow state), and meta-memory (strategic self-awareness).
   See [[memory]] for the full treatment.
9. **Learning and Adaptation** — the Reflexion pattern generates, critiques,
   stores an insight, and retries. The ACE loop scales this to system level
   through a Generator, a Reflector, and a Curator that updates a persistent
   playbook file.
10. **Model Context Protocol (MCP)** — a universal client-server standard for
    agent-tool integration. MCP separates Resources (read-only context) from
    Tools (executable actions) and supports on-demand tool discovery. See
    [[mcp]].
11. **Goal Setting and Monitoring** — the Observe phase of the agent loop
    compares the environmental result of an action against the objective.
    Structured notes and stopping conditions prevent runaway loops.

### Part Three: Resilience and Knowledge

Three patterns form a resilience triad: recovery from failure, the boundary
between machine autonomy and human oversight, and access to evidence the model
was never trained on.

12. **Exception Handling and Recovery** — a fallback chain of primary
    handler, fallback handler, and response agent. Error classification
    (transient, permanent, logic, resource) determines whether the agent
    retries, switches tools, replans, or stops.
13. **Human-in-the-Loop** — three oversight tiers on a reversibility
    framework. HITL requires pre-approval for every action. HOTL monitors
    with intervention capability. HIC grants autonomy with an emergency stop.
    Reversible actions proceed autonomously; irreversible actions demand a
    mandatory approval gate.
14. **Knowledge Retrieval (RAG)** — retrieve relevant documents, augment the
    prompt with them, and generate a response grounded in that evidence
    rather than training data. Retrieval strategy (dense, sparse, hybrid) and
    chunking strategy determine retrieval quality.

### Part Four: Advanced Patterns for Production

Seven patterns address production demands: networking, cost, reasoning,
security, evaluation, prioritisation, and knowledge generation.

15. **Inter-Agent Communication (A2A)** — an open, HTTP-based protocol that
    lets agents on different frameworks discover and delegate to each other
    through a published Agent Card. Where MCP connects an agent to tools, A2A
    connects agents to agents.
16. **Resource-Aware Optimisation** — match token spend, latency, and compute
    to task requirements through model routing, context efficiency
    techniques, the agents-versus-workflows distinction, and caching.
17. **Reasoning Techniques** — Chain of Thought and Extended Thinking make
    the model's reasoning visible before it produces a response. Claude's
    effort parameter (low, medium, high, max) matches reasoning depth to
    task demand.
18. **Guardrails and Safety Patterns** — defence against indirect prompt
    injection, memory-poisoning attacks such as MINJA and AgentPoison, and
    self-replicating attacks such as ClawWorm. Defence in depth: context
    privilege isolation, configuration integrity verification, zero-trust
    tool execution, and composite trust scoring.
19. **Evaluation and Monitoring** — LLM-as-Judge scores output against a
    rubric. Trajectory evaluation measures action validity, loop rate, and
    plan adherence, not just final output. See [[evaluation]].
20. **Prioritisation** — an urgency-importance matrix orders competing
    demands. Dynamic re-prioritisation adjusts the queue as conditions
    change; token budgets scale with priority.
21. **Exploration and Discovery** — curiosity-driven queries and
    hypothesis-testing loops let an agent generate knowledge it was not
    asked for. Production systems bound the exploration budget, typically
    around 10% of token spend.

Chapter 22 closes the book by composing these 21 patterns into four reference
architectures: a customer service agent, a research agent, a coding agent
(Claude Code), and an enterprise workflow agent. No production system uses one
pattern alone.

## Code

This guide strips code deliberately. Gulli's book carries working
implementations in LangChain/LangGraph, CrewAI, and Google ADK for every
pattern. Consult the source book for runnable examples. The value of this
guide is the concept map; the value of the book is the implementation.

## Verification

A reader has understood a pattern when they can state two things without
looking it up:

- **Its trigger condition** — the symptom that tells a builder this pattern
  is needed now. Routing triggers on heterogeneous input types. Multi-Agent
  Collaboration triggers on one of three signals: an overloaded system
  prompt, consistent wrong-tool selection, or a context window that drowns
  in tokens.
- **Its trade-off** — the cost the pattern buys against. Prompt Chaining
  buys accuracy with latency. Reflection buys quality with token spend. RAG
  buys grounding with retrieval cost and re-ranking complexity.

A reader who can name the pattern but not its trigger or its trade-off has
memorised a label, not learned a pattern.

## Common Pitfalls

- **Premature multi-agent adoption.** Start with a single agent. Maximise it
  through better prompts and tools. Split only when the system prompt is
  overloaded with conditional logic, the agent keeps selecting the wrong
  tool, or the context window loses critical information.
- **Reflection without grounding.** An agent that critiques its own
  hallucinated output, with no external evidence to check against, may
  conclude the hallucination is correct and produce a more confident wrong
  answer. Pair Reflection with RAG or Tool Use.
- **Treating memory as equal-weight semantic search.** A six-month-old
  instruction can contradict yesterday's update. Without temporal decay,
  stale memories contaminate fresh decisions, and this is the same
  vulnerability that MINJA-style attacks exploit to plant persistent
  adversarial instructions.
- **Deploying RAG without re-ranking.** Initial retrieval returns false
  positives. Without a re-ranking pass, the model either ignores irrelevant
  documents, wasting tokens, or incorporates them, degrading answer quality.

## Related

- [[the-agent-loop]]
- [[tool-use]]
- [[memory]]
- [[planning-and-reasoning]]
- [[supervisor-worker-multi-agent]]
- [[mcp]]
- [[reflexion]]
- [[react]]
- [[plan-and-execute]]
- [[workflow-vs-autonomous-agent]]

## Sources

- [[10_Sources/Books/agentic-design-patterns-gulli-2025|Agentic Design Patterns (Gulli)]]

## See also

- [[MOC - Agent Patterns]]
