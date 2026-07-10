---
type: concept
status: draft
created: 2026-07-10
name: Best Practices Index
slug: best-practices-index
topic:
- topic/best-practices
tags: [index, engineering-principles]
synonyms: [engineering principles, agent best practices]
defined_in: "[[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]"
related_concepts: ["[[anti-patterns-index]]", "[[the-agent-loop]]", "[[evaluation]]"]
anthropic: true
---

# Best Practices Index

> A curated index of engineering principles that hold up when agents reach production.

## Summary

This note indexes the principles that make agents reliable. Anthropic's guidance sets the spine: keep the design simple, make the agent transparent, and craft the agent-computer interface with care. Each principle below carries a one-line rationale and a wikilink to its fuller note. The index grows as each principle earns a dedicated page.

## Principles

- **Small, focused agents** — A narrow scope cuts error compounding and eases testing. See [[workflow-vs-autonomous-agent]].
- **Tool-first design** — A clear, documented tool surface beats clever prompting. See [[tool-use]].
- **Deterministic workflows** — Fixed code paths suit well-defined tasks and give predictable results. See [[plan-and-execute]].
- **Structured outputs** — Typed, schema-bound outputs let downstream code parse without guesswork. See [[tool-use]].
- **Observable execution** — Log the full trajectory so a human reads what the agent did. See [[the-agent-loop]].
- **Minimal prompting** — Start with one focused prompt plus retrieval and examples; add complexity only when it pays. See [[prompt-engineering]].
- **Checkpointing** — Save state at each step so a run resumes rather than restarts. See [[memory]].
- **Human oversight** — A human reviews code and high-stakes actions before they land. See [[supervisor-worker-multi-agent]].
- **Evaluation-first development** — Write evals early and run them on every change. See [[evaluation]].
- **Security by design** — Sandbox tool calls, validate input, and grant least privilege. See [[tool-use]].
- **Cost-aware engineering** — Agents trade latency and tokens for autonomy; measure the trade before you pay it. See [[workflow-vs-autonomous-agent]].

## Detail

Anthropic frames three governing principles. Maintain simplicity in the agent's design. Prioritise transparency through explicit planning steps. Craft the agent-computer interface with thorough tool documentation and testing. The principles above expand that spine into engineering practice.

Boris Cherny's Claude Code work confirms the pattern. Plain glob and grep, driven by the model, beat a vector database. Simplicity won.

## Trade-offs and Limits

Simplicity helps most tasks. A genuinely open-ended problem still needs an autonomous agent, and that agent costs more. Choose the workflow when the path is known.

## Related

- [[anti-patterns-index]]
- [[the-agent-loop]]
- [[evaluation]]
- [[workflow-vs-autonomous-agent]]

## Sources

- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]] — https://www.anthropic.com/engineering/building-effective-agents
- [[10_Sources/Interview/boris-cherny-pragmatic-engineer|Building Claude Code with Boris Cherny]] — https://newsletter.pragmaticengineer.com/p/building-claude-code-with-boris-cherny

## See also

- [[MOC - Best Practices]]
