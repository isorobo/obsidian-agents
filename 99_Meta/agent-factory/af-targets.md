---
type: meta
title: Agent-factory target vocabulary (af_targets)
status: permanent
created: 2026-10-04
topic:
- topic/meta
tags:
- agent-factory
- af-targets
- wiki-agents
wiki_role: meta
---

# Agent-factory target vocabulary

Controlled list of values for the `af_targets` frontmatter field (`99_Meta/schema.md` section 2.9).
Each value names one item in the user's agent-factory project (`af:`) or its sibling code-factory
(`cf:`) that a vault note bears on. The `wiki-agents-monitor` sets `af_targets` on every note it
writes, and `/wiki-agents af-tag` sets it on notes that lack it. `/wiki-agents digest` groups notes
by these IDs in `99_Meta/agent-factory-digest/`.

Information flows one way. Agent-factory never reads this vault and never depends on it. The digest
is a reading list the user acts on by choice; nothing here writes into agent-factory or code-factory.

A new ID requires an edit to this note first, by the user. Tools never invent an ID.

## Format

One bullet per ID: the ID in backticks, then a short gloss. Tools parse the backticked token at
the start of each bullet under the ID headings below and ignore all other text.

## Assignment rules

1. Assign an ID only when the note's own content concretely informs, tests, or contradicts that
   item. Shared vocabulary alone ("agents", "tools") is not enough.
2. Assign at most 5 IDs per note. Prefer the most specific ID.
3. `af:RSCH-01/<item>` only when the note is a primary source for that corpus item, or a direct
   study of it (its repository, paper, specification or official documentation).
4. `af:RSCH-04/Qnn` when the note supplies evidence toward a written answer to question nn.
5. `af:BI-11` and `af:BI-13` only for material on tool-call timeouts or live cancellation.
6. `cf:` IDs only for material that bears on code-factory itself, such as a Claude Code or
   OpenHands release that changes the CLI, flags, output format or API an adapter relies on.
7. `none` alone when nothing applies. Never combine `none` with another ID.

## Agent-factory ADRs (docs/adr/)

- `af:ADR-0001` What an agent is: minimum definition, agent versus LLM call.
- `af:ADR-0002` Two planes, two enforcement points: control plane versus intelligence plane.
- `af:ADR-0003` Model port: how models and runtimes are invoked and substituted.
- `af:ADR-0004` Action / capability boundary: tools as capabilities, the action gate, worker kinds.
- `af:ADR-0005` State, context, memory: what is durable, what is context, what memory is.
- `af:ADR-0006` Persistence and recovery: crash survival, resume, checkpoints.
- `af:ADR-0007` Governance and human authority: approvals, human gates, policy ownership.
- `af:ADR-0008` Evaluation and evidence: success criteria, evaluators, provenance.
- `af:ADR-0009` Factory semantics and the Code Factory relationship.

## Agent-factory v2 requirements (.planning/milestones/v1-REQUIREMENTS.md)

- `af:REAL-01` Reference Research Agent on a real model adapter with read-only research tools.
- `af:REAL-02` Two or more real provider adapters run the same agent definition unchanged.
- `af:REAL-03` Project-extension example: a new agent outside the core with its own tools, policies, context sources and evaluators.
- `af:DELEG-01` Delegation to a subagent with propagated permissions, budgets, isolated state and parent-visible evidence.
- `af:DELEG-02` MCP adapter for external tool servers.
- `af:DELEG-03` Reflection as an optional agent capability.
- `af:SUBS-01` Shared substrate beneath Agent Factory and Code Factory, only after both have running evidence.

## RSCH-01 corpus study notes (one per corpus item)

- `af:RSCH-01/12-factor-agents` 12-Factor Agents (github.com/humanlayer/12-factor-agents).
- `af:RSCH-01/learn-agent-architecture` learn-agent-architecture (github.com/hardness1020/learn-agent-architecture).
- `af:RSCH-01/mini-swe-agent` mini-SWE-agent (github.com/SWE-agent/mini-swe-agent).
- `af:RSCH-01/smolagents` Hugging Face smolagents (github.com/huggingface/smolagents).
- `af:RSCH-01/react` ReAct (Yao et al., arXiv 2210.03629).
- `af:RSCH-01/reflexion` Reflexion (Shinn et al., arXiv 2303.11366).
- `af:RSCH-01/generative-agents` Generative Agents (Park et al. 2023, arXiv 2304.03442).
- `af:RSCH-01/mcp` Model Context Protocol, as the agent/environment boundary.
- `af:RSCH-01/claude-code` Claude Code, where inspectable (docs, changelog, SDK, public repos).

## RSCH-04 research questions (.planning/BRIEF.md section 26)

- `af:RSCH-04/Q01` What is the minimum definition of an AI agent?
- `af:RSCH-04/Q02` What distinguishes an agent from an LLM call?
- `af:RSCH-04/Q03` What distinguishes an agent runtime from an agent definition?
- `af:RSCH-04/Q04` What should the Factory own?
- `af:RSCH-04/Q05` What should the model own?
- `af:RSCH-04/Q06` What should tools own?
- `af:RSCH-04/Q07` What should policy own?
- `af:RSCH-04/Q08` What should humans own?
- `af:RSCH-04/Q09` What state must be durable?
- `af:RSCH-04/Q10` What state must never be durable?
- `af:RSCH-04/Q11` What is memory?
- `af:RSCH-04/Q12` What is context?
- `af:RSCH-04/Q13` What is an observation?
- `af:RSCH-04/Q14` What is an action?
- `af:RSCH-04/Q15` What is a capability?
- `af:RSCH-04/Q16` What constitutes a tool?
- `af:RSCH-04/Q17` What constitutes delegation?
- `af:RSCH-04/Q18` What constitutes success?
- `af:RSCH-04/Q19` What constitutes evidence?
- `af:RSCH-04/Q20` What is the minimum useful evaluation architecture?
- `af:RSCH-04/Q21` What must survive a process crash?
- `af:RSCH-04/Q22` How should an agent resume?
- `af:RSCH-04/Q23` How should agents be isolated?
- `af:RSCH-04/Q24` How should agents communicate?
- `af:RSCH-04/Q25` What should a parent agent know about a child agent?
- `af:RSCH-04/Q26` How should permissions propagate?
- `af:RSCH-04/Q27` How should budgets propagate?
- `af:RSCH-04/Q28` How should human approval interact with execution?
- `af:RSCH-04/Q29` How should different models/runtimes be substituted?
- `af:RSCH-04/Q30` Which abstractions are genuinely universal?
- `af:RSCH-04/Q31` Which abstractions are merely implementation patterns?
- `af:RSCH-04/Q32` What should remain project-specific?
- `af:RSCH-04/Q33` What should remain outside Agent Factory entirely?

## Agent-factory open break-it items (docs/evidence/BREAK-IT-LEDGER.md)

- `af:BI-11` Timeouts enforced on model calls only, never on tool calls (accepted limitation in V0).
- `af:BI-13` No CLI-reachable, mid-step, external cancellation signal for a running run (accepted limitation in V0).

## Code-factory ADRs (code-factory docs/adr/)

- `cf:ADR-0001` Foundation schema.
- `cf:ADR-0002` Operational store and implementation language.
- `cf:ADR-0003` Protocol v0 and runtime qualification.
- `cf:ADR-0004` Tiers as profiles and the QUICK gate.
- `cf:ADR-0005` Threat model and verifier independence.
- `cf:ADR-0006` Roadmap re-cut and register re-partition.
- `cf:ADR-0007` Delivery pipeline skills.
- `cf:ADR-0008` Proactive security by design.
- `cf:ADR-0009` Run instruction discipline and the repeated-waiver signal.
- `cf:ADR-0010` Plan-time domain contracts.
- `cf:ADR-0011` External skill adaptation and provenance policy.
- `cf:ADR-0012` Skill contract, invocation class, and composition rules.
- `cf:ADR-0013` Strix as a coordinator-run security evidence producer under Factory governance.
- `cf:ADR-0014` QUICK candidate identity and the amendment mechanism.

## Code-factory runtime adapters (code-factory adapters/)

- `cf:adapter/claude-code` Claude Code adapter: `claude -p` stream-json invocation, tool allowlists, auth behaviour.
- `cf:adapter/openhands` OpenHands adapter: network client over HTTP or WebSocket.

## No target

- `none` Nothing in agent-factory or code-factory is informed by this note.
