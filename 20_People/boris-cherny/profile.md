---
type: person
status: stub
created: 2026-07-10
name: Boris Cherny
slug: boris-cherny
kind: person
role: Head of Claude Code, Anthropic
affiliations: [Anthropic, Meta]
topic:
- topic/boris-cherny
tags: [claude-code, engineering-leader]
key_sources: ["[[10_Sources/Interviews/boris-cherny-pragmatic-engineer|Building Claude Code with Boris Cherny]]"]
---

# Boris Cherny

> Boris Cherny created and leads Claude Code at Anthropic, and his engineering principles shape how the team builds agents.

## Role

Boris Cherny is Head of Claude Code at Anthropic. He joined in September 2024 on the Labs team and built Claude Code from a terminal prototype. He spent five years at Meta as a Principal Engineer on infrastructure and developer experience. He authored the book *Programming TypeScript*.

## Contribution to Agent Engineering

Cherny's public talks and interviews yield reusable principles, extracted below rather than merely linked.

- **Simplicity wins the search problem** — Plain glob and grep, driven by the model, beat a local vector database and recursive model-based indexing. Prefer the simple tool the model already understands.
- **Bet on the model, not the moment** — The team built Claude Code for where the model would be, not where it was. Design for the trajectory of capability.
- **Keep the agent loop simple** — Plan first, refine the plan, then execute. A solid plan lets the model one-shot the implementation almost every time.
- **Finish every migration** — A half-finished migration confuses humans and models both. Complete a change once you start it.
- **Automate repeated decisions** — After a review comment recurs three or four times, encode it as a lint rule. Remove the manual burden.
- **Fix the foundation first** — Stable infrastructure gives higher leverage than a feature on shaky ground.
- **Prototype over specification** — The team built dozens of working prototypes rather than static mocks or a PRD.
- **Underfund a little** — Small teams lean on Claude, which sharpens the product and the workflow.

## Key Positions

- Code quality carries a measurable, double-digit-percent impact on engineering productivity.
- Optimise late; premature optimisation wastes effort before the shape is known.
- Modern engineering rewards fast context switching across parallel agent sessions.

## Timeline

- 2019 — Joins Meta as a Principal Engineer.
- September 2024 — Joins Anthropic on the Labs team.
- 2024 — Builds Claude Code as a terminal prototype.
- 2026 — Leads Claude Code as its head.

## Status

This profile is a stub. It captures principles from one primary interview. A full extraction run across his talks and posts remains pending.

## Key Sources

- [[10_Sources/Interviews/boris-cherny-pragmatic-engineer|Building Claude Code with Boris Cherny]] — https://newsletter.pragmaticengineer.com/p/building-claude-code-with-boris-cherny

## Related

- [[claude-code]]
- [[claude-agent-sdk]]
- [[best-practices-index]]

## See also

- [[MOC - Boris Cherny]]
