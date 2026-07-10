---
type: source
status: draft
created: 2026-07-10
title: "Agents Part II: How to Design an Agent: Architectures, Protocols, and Technical Evaluation"
authors:
- Michael J Bommarito II
- Daniel Martin Katz
- Jillian Bommarito
organisation: 
source_type: book
venue: "Working draft chapter, Artificial Intelligence for Law and Finance (forthcoming textbook)"
url: https://github.com/mjbommar/ai-law-finance-book/
year: 2025
date_published: 2025-12-20
anthropic: false
topic:
- topic/architectures
- topic/domain-applications
tags: [mcp, a2a, agent-architecture, technical-evaluation, multi-agent, legal-ai]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Agents Part II: How to Design an Agent: Architectures, Protocols, and Technical Evaluation

> Full citation: Bommarito II, M.J., Katz, D.M. and Bommarito, J. "Agents Part II: How to Design an Agent: Architectures, Protocols, and Technical Evaluation." Working draft chapter, Artificial Intelligence for Law and Finance, 2025. https://github.com/mjbommar/ai-law-finance-book/

## Summary

The chapter builds agent architecture around a "Ten Questions" framework, a control-loop sequence running Triggers, Intent, Perception, Action, Memory, Planning, Termination, Escalation, Delegation, and Governance. Each question gets its own numbered section, and each section pairs an architectural concept with parallel legal and financial examples, such as a transactional lawyer reviewing a credit agreement beside a portfolio manager rebalancing a book. The Perception section introduces the Model Context Protocol (MCP) as the standard that lets an agent reach external tools and data without bespoke integration per source, splitting its surface into read-only Resources, state-changing Tools, and procedure-encoding Prompts. The Delegation section introduces the Agent-to-Agent Protocol (A2A) as the complementary standard for agent-to-agent work assignment, built around Agent Cards, Tasks, and Artifacts. The chapter states a plain decision rule: MCP for well-defined, auditable operations measured in seconds; A2A for delegated work requiring specialist judgement, measured in minutes to hours; both together for complex end-to-end workflows such as due diligence or regulatory assessment. Technical evaluation appears throughout as a per-capability discipline rather than a single closing section: each architectural question closes with its own evaluation criteria, for example five criteria for trigger systems and six for escalation mechanisms. The chapter closes its architectural arc by arguing that governance cannot be retrofitted, and that logging, override mechanisms, state snapshots, privilege enforcement, and escalation hooks must be designed in from the start.

## Key Concepts

- The Ten Questions framework sequences agent design as Triggers, Intent, Perception, Action, Memory, Planning, Termination, Escalation, Delegation, and Governance.
- MCP standardises how an agent reaches tools and data; A2A standardises how an agent delegates work to another agent.
- MCP splits into three primitives: Resources (read-only), Tools (state-changing), and Prompts (procedure templates).
- A2A structures delegation around Agent Cards, Tasks, and Artifacts, moving through discovery, delegation, execution, delivery, and completion.
- Multi-agent systems compose three patterns: sequential, parallel, and hierarchical delegation, each with a distinct tradeoff.
- Governance cannot be retrofitted; logging, override mechanisms, state snapshots, privilege enforcement, and escalation hooks are architectural decisions, not policy add-ons.
- Evaluation is distributed across the architecture: each capability area (triggers, perception, action, escalation) carries its own evaluation criteria rather than one general-purpose eval suite.

## Terminology

- **Trigger** — "the events that start agent execution."
- **Channel** — "the pathway through which that event reaches the agent," distinct from a trigger as the how versus the trigger's what.
- **Interaction surface** — the user experience modality through which humans engage with an agentic system, a UX concept distinct from the architectural concepts of trigger and channel.
- **Instruction, Intent, Goal, Task** — a four-stage pipeline. Instruction is "the raw input that starts the process." Intent is "the underlying purpose, constraints, and success criteria behind an instruction." Goal is "the machine-readable specification that intent points toward." A task is "the concrete unit of work the agent executes to advance a goal."
- **Perception tools** — "the interfaces through which an agent observes the world beyond its training data."
- **MCP Host, Client, Server** — the Host "manages the agent and controls what it can access," analogous to an IT department; the Client is "the agent-side component that discovers available tools and makes requests"; the Server is what each information source runs "to expose its capabilities through the standard interface."
- **MCP Resources** — "read-only data access endpoints," such as document repositories or market data feeds.
- **MCP Tools** — "executable functions that change state," such as filing a document or submitting a trade.
- **MCP Prompts** — "reusable templates for common tasks" that "encode Standard Operating Procedures."
- **Agent-to-Agent Protocol (A2A)** — the protocol that "standardizes how agents delegate work to each other," using Agent Cards to list capabilities, Tasks to define delegated work, and Artifacts as returned deliverables.
- **Idempotency** — "an operation is idempotent if performing it multiple times produces the same result as performing it once."
- **In-context learning (ICL)** — "the ability of large language models to learn from information provided in their input, without any update to the model's underlying parameters," distinct from weight-updating machine learning.
- **Retrieval-Augmented Generation (RAG)** — "a prompt pattern, not a software system or mathematical technique," following a retrieve, augment, generate sequence, and stated to be retrieval-method-agnostic.

## Architecture and Implementation

The chapter's spine is the Ten Questions framework, and this section is the chapter's own subject, so it repays the deepest treatment here.

**Triggers, channels, and surfaces (Section 2).** A trigger is the event that demands attention; a channel is the pathway that event travels. Four channel types cover almost all work intake: external feeds, human prompts, scheduled jobs, and escalation events, illustrated against named legal and financial systems such as CM/ECF, PACER, EDGAR, Bloomberg, and Westlaw. A separate concept, the interaction surface, captures the user experience dimension along four axes: synchronicity, initiative, embodiment, and output format, sorted into three primary surface types: conversational, automation, and document. Evaluation of a trigger system rests on five criteria: coverage, latency, reliability, priority, and auditability.

**Intent (Section 3).** A four-stage pipeline, instruction to intent to goal to task, replaces rule-based routing with LLM-based semantic classification. A stakes-versus-ambiguity decision matrix governs when the agent should proceed, confirm, or clarify before acting.

**Perception and the Model Context Protocol (Section 4).** Perception tools split into three categories: information retrieval, document processing, and computation. In-context learning is the mechanism that makes any retrieved content useful at all, since the model adapts its output to whatever sits in its context window; retrieval-augmented generation is the associated prompt pattern, and a vector store is the infrastructure that makes similarity search practical at scale, explicitly distinguished from RAG itself. MCP enters here as the standardisation layer for perception. The chapter frames the pre-MCP world as one of bespoke, per-source integrations, growing without bound as agents and tools multiply, and states the payoff in integration-count terms: connecting ten agents to ten tools needs 100 custom integrations without MCP, but only 20 implementations with it, since each agent and each tool learns the protocol once. The chapter cites a benchmark finding over ten thousand MCP servers already in the ecosystem. Architecturally, MCP composes three roles: a Host that manages the agent and controls access, a Client that discovers available tools and makes requests, and a Server that each information source runs to expose its capabilities through the standard interface. For perception specifically, MCP defines Resources as read-only data access endpoints; the read-only designation lets an agent retrieve a document without being able to modify or file it, which mirrors how organisations already structure permissions. The chapter does not descend to transport-layer detail; it gives no stdio-versus-HTTP-or-SSE comparison, no JSON-RPC message schema, and no discovery-handshake sequence, staying at the architectural and governance level suited to a law-and-finance reader rather than a protocol implementer.

**Action and MCP's action-side primitives (Section 5).** Action tools carry a reversibility framework that maps reversibility tiers to oversight mechanisms: post-hoc review, checkpoint review, pre-approval, or multi-party approval. Section 5.4 extends MCP into the action side through two further primitives. MCP Tools are executable functions that change state, distinct from read-only Resources; the chapter's key technical pattern here is embedding risk metadata directly in the tool manifest, covering reversibility classification, approval requirements, and audit logging needs, so the MCP Host can enforce controls automatically rather than through bespoke per-tool logic. MCP Prompts are reusable templates that encode standard operating procedures, illustrated with contract review checklists and filing preparation workflows on the legal side, and trade compliance checks and client onboarding sequences on the finance side; the chapter describes prompts as guardrails that keep the agent inside an approved procedure for high-stakes actions. Section 5.5 sets out action security controls, naming three specific threats with mitigations: prompt injection through action parameters, privilege escalation through tool chaining, and action replay, the last addressed through idempotency and nonces or timestamps.

**Memory, planning, termination, and escalation (Sections 6 to 9).** These sections cover retrieval-augmented memory with matter and client isolation, planning patterns with an explicit budget architecture and stopping conditions, termination criteria including a named "reliability cliff" and graceful degradation, and escalation categories, budget exhaustion, low confidence, approval requirements, and errors or anomalies, each evaluated on six criteria: coverage, calibration, latency, routing, context quality, and response handling.

**Delegation and the Agent-to-Agent Protocol (Section 10).** Multi-agent architecture is motivated by the same reasoning a law firm or trading desk already uses to staff a matter: no single person, or single agent, holds every needed skill. Delegation is defined as agent-to-agent work assignment, distinct from escalation's agent-to-human direction; the coordinator defines what needs doing, the specialist determines how. A2A is introduced as the delegation-side counterpart to MCP's tool-access standardisation: "Just as MCP standardizes how agents access tools, the Agent-to-Agent Protocol (A2A) standardizes how agents delegate work to each other." A2A borrows professional vocabulary directly: Agent Cards list capabilities, like a specialist's credentials; Tasks define delegated work, like an engagement letter specifying scope, constraints, and escalation triggers; Artifacts are the deliverables returned on completion. Its lifecycle runs discovery, delegation, execution, delivery, and completion, which the chapter states ensures delegated work stays scoped, tracked, and auditable.

Three multi-agent patterns organise how delegation composes: sequential delegation chains agents in order, simple to debug but slow, since each stage waits on the last; parallel delegation runs independent specialists concurrently, trading coordination overhead for speed; hierarchical delegation nests sub-delegation inside a lead agent, enabling deep decomposition at the cost of harder debugging when a failure sits deep in the tree. Most production systems blend these patterns rather than choosing one.

The chapter states a direct protocol selection rule in a comparison table: use MCP for immediate, well-defined, auditable operations measured in seconds, such as querying a database or retrieving a document; use A2A for delegated work requiring judgement, measured in minutes to hours, such as assigning research or coordinating specialists; use both together for end-to-end workflows such as due diligence, portfolio rebalancing, or regulatory assessment. As of late 2025, the chapter states MCP as production-ready while A2A is "maturing with variable cross-vendor reliability," and recommends designing fallbacks to human coordination for critical decisions until A2A standardisation solidifies.

**Governance as architecture (Section 11).** The chapter argues governance policy and governance-aware architecture are distinct: policy defines what controls are required, architecture provides the technical foundation that makes those controls possible, and that foundation cannot be added after the fact. Five architectural patterns enable governance: a structured logging schema spanning trigger, intent, perception, reasoning, action, memory, and delegation events; override and circuit-breaker patterns, including a named "red button" emergency stop that must sit outside agent memory and be triggerable through an out-of-band channel; state snapshots supporting reproducibility, rollback, and resumability; privilege enforcement; and escalation hooks.

## Code Examples

The chapter shows no MCP wire-protocol code; no JSON-RPC messages, transport configuration, or discovery-handshake sequence appear anywhere in the pages examined. The code that does appear illustrates general tool design principles from Section 4.6, applicable to MCP tool and resource implementations without being MCP-specific syntax. A poor design bundles responsibilities into one untyped function, for example a single `legal_research(query: str) -> dict` that returns an unspecified dictionary. A better design separates responsibilities and types each return, for example distinct `search_cases`, `retrieve_case`, `shepardize`, and `format_citation` functions each returning a specific type such as `list[Citation]` or `CaseText`. A graceful-failure pattern returns a structured error object, for example a `CaseNotFoundError` model carrying a reason and suggestions, rather than raising a bare exception, so the agent can report a missing authority explicitly instead of proceeding silently.

## Best Practices

Tool design should follow single responsibility, one function per tool, avoiding bundled or untyped calls. Failure should be graceful: a tool should return a typed error object carrying diagnostic detail rather than raise a bare exception, since in professional practice this prevents an agent from proceeding silently past a gap in its authority. Access should follow least privilege: a research tool needs read access to case databases, not write access to a document management system, so a compromised agent's damage stays limited to disclosure rather than destruction. MCP Tool manifests should carry risk metadata directly, reversibility classification, approval requirements, and audit logging needs, so the Host can enforce controls automatically. Action tools should be idempotent by design, through unique transaction identifiers, or provide an explicit confirmation mechanism, since a retry against a non-idempotent tool risks a duplicate payment or a duplicate filing. Delegation should carry complete logging of the delegation contract, the specialist's identity, and the returned artifact, so an audit trail can span the entire delegation tree. Until A2A standardisation solidifies, the chapter recommends a fallback to human coordination for critical delegated decisions.

## Warnings and Anti-Patterns

The chapter names three action-security threats with mitigations. Prompt injection through action parameters lets an adversary embed malicious instructions in data the agent passes to a tool; the mitigation sanitises all parameters and never passes raw user input directly to a sensitive action interface. Privilege escalation through tool chaining lets an agent combine several low-privilege tools into a high-privilege outcome; the mitigation analyses tool combinations and requires approval for any sequence crossing a security boundary. Action replay lets an attacker capture and resubmit a valid action request; the mitigation requires nonces or timestamps so each request processes once only. At the multi-agent level, the chapter names three coordination failure modes: deadlock, where agents wait on each other cyclically; divergence, where specialists reach incompatible conclusions requiring reconciliation; and cascading errors, where an incorrect output propagates through the system uncorrected. Prevention requires timeouts, validation at each handoff, and clear escalation paths. On governance, the chapter states plainly that a system designed without audit logging cannot suddenly produce compliance reports, and that circuit-breaker state must sit external to the agent, since an agent cannot be trusted to halt itself reliably.

## Related Concepts

- [[mcp]]
- [[claude-agent-sdk]]
- [[tool-use]]
- [[the-agent-loop]]
- [[supervisor-worker-multi-agent]]
- [[evaluation]]
- [[what-is-an-agent-bommarito-2025]]
- [[governing-ai-agents-risk-bommarito-2025]]

## Future Work

The pages examined for this note cover the Introduction through Section 11 (Governance) but stop short of Section 12 (Conclusion), which synthesises the chapter's tradeoffs. A full technical-evaluation methodology, if the chapter states one beyond the per-capability criteria distributed through Sections 2 to 9, would sit near the chapter's close and merits a follow-up read. The companion volume, Governing Agents, is cited repeatedly as the source for the policy layer this chapter's architecture is designed to support: the five-layer regulatory framework, dimensional calibration, delegation authorisation, identity management, and retention requirements.

## References

- Bommarito II, M.J., Bommarito, J. and Katz, D.M. "Agents Part I: What is an Agent? A Conceptual Primer and History." Working draft chapter, Artificial Intelligence for Law and Finance, 2025.
- Anthropic. Model Context Protocol announcement. 2024.
- "Model Context Protocol Specification." 2025.
- "Agent2Agent Protocol Specification." 2025.
- Google Developers. Agent-to-Agent Protocol. 2025.
- Mo et al. Benchmark of MCP server ecosystem scale. 2025.
- Brown et al. In-context learning in large language models. 2020.
- Lewis et al. Retrieval-Augmented Generation. 2020.
- Wu et al. Motivations for multi-agent design. 2023.
- Guo et al. Motivations for multi-agent design. 2024.
- Wang et al. Multi-agent collaboration patterns. 2024c.
- Cemri et al. Multi-agent failure modes. 2025.
- OWASP Foundation. Action security threat taxonomy. 2025.
- Liu et al. Prompt injection and tool-chaining threats. 2024.
- OpenID Foundation AI Identity Management Community Group. Agent identity and delegation logging. 2024.
- McCarthy, J. and Hayes, P. The frame problem. 1969.
- Austin, J.L. Performative utterances. 1962.
