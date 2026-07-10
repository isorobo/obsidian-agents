---
type: concept
status: draft
created: 2026-07-10
name: Anti-Patterns Index
slug: anti-patterns-index
topic:
- topic/anti-patterns
tags: [index, failure-modes]
synonyms: [failure modes, agent anti-patterns]
defined_in: "[[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]"
related_concepts: ["[[best-practices-index]]", "[[evaluation]]", "[[the-agent-loop]]"]
anthropic: true
---

# Anti-Patterns Index

> A curated index of the failure modes that break agents in production.

## Summary

This note indexes recurring failure modes. Each entry names a symptom and points to the fix. Anthropic's core warning frames the list: added complexity buys worse debugging, not better results. Reach for a simple solution first. The wikilinks route to the practice or concept that resolves each failure.

## Anti-patterns

- **Overly autonomous agents** — Symptom: the agent wanders and compounds errors. Fix: [[workflow-vs-autonomous-agent]].
- **Prompt spaghetti** — Symptom: one giant prompt mixes many jobs. Fix: [[prompt-engineering]].
- **Tool explosion** — Symptom: dozens of overlapping tools confuse selection. Fix: [[tool-use]].
- **Hidden state** — Symptom: state lives outside the transcript and defies inspection. Fix: [[memory]].
- **Poor observability** — Symptom: a failed run leaves no trace to read. Fix: [[the-agent-loop]].
- **Lack of evaluation** — Symptom: regressions ship undetected. Fix: [[evaluation]].
- **Context overload** — Symptom: the window fills with noise and the model loses the thread. Fix: [[memory]].
- **Hallucinated planning** — Symptom: the agent invents steps that reference nothing real. Fix: [[planning-and-reasoning]].
- **Unbounded recursion** — Symptom: the loop repeats with no stop condition. Fix: [[the-agent-loop]].
- **Fragile prompts** — Symptom: a small wording change breaks behaviour. Fix: [[prompt-engineering]].
- **Tight coupling** — Symptom: agent logic binds to one model or one tool version. Fix: [[best-practices-index]].
- **Poor memory management** — Symptom: the agent forgets or re-reads the same facts. Fix: [[memory]].
- **Lack of testing** — Symptom: no eval set guards changed behaviour. Fix: [[evaluation]].

## Detail

Framework abstractions hide the underlying prompts and responses. That layer complicates debugging and tempts teams to add complexity a simpler path would avoid. Anthropic advises the reverse. Start with an optimised single call. Increase complexity only when a simpler solution falls short.

Cherny's rule reinforces the point on migrations. Finish a migration once you start it. A half-finished migration confuses humans and models both.

## Trade-offs and Limits

Some complexity earns its keep. A multi-agent system suits a genuinely parallel research task. The test stays constant: does the added structure improve a measured outcome.

## Related

- [[best-practices-index]]
- [[evaluation]]
- [[the-agent-loop]]
- [[tool-use]]

## Sources

- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]] — https://www.anthropic.com/engineering/building-effective-agents
- [[10_Sources/Interview/boris-cherny-pragmatic-engineer|Building Claude Code with Boris Cherny]] — https://newsletter.pragmaticengineer.com/p/building-claude-code-with-boris-cherny

## See also

- [[MOC - Anti-Patterns]]
