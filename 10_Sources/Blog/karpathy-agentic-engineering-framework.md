---
type: source
status: draft
created: 2026-07-11
title: "Agentic Engineering: Karpathy's New Framework"
authors:
- AI Builder Club
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 1.9 (commentary on Andrej Karpathy's 30 April 2026 Sequoia Ascent talk)
url: https://www.aibuilderclub.com/blog/karpathy-agentic-engineering
year: 2026
date_published: 2026-05-27
anthropic: false
topic:
- topic/best-practices
- topic/karpathy
tags:
- karpathy
- agentic-engineering
- vibe-coding
- course
nlm_id:
nlm_skip: false
watchlist_channel:
af_targets:
- af:ADR-0008
- af:RSCH-04/Q18
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: dd4b9339a5f0cb400562eb4e310280bba488c7a5b62b203051eb7eb9f08f9a2d
---

# Agentic Engineering: Karpathy's New Framework

> AI Builder Club, "Agentic Engineering: Karpathy's New Framework", Build AI Agents Course, 27 May 2026, https://www.aibuilderclub.com/blog/karpathy-agentic-engineering. AI Builder Club's commentary on Andrej Karpathy's 30 April 2026 Sequoia Ascent talk, not Karpathy's original words.

## Summary

Karpathy draws a line between vibe coding — rapid, low-oversight AI-assisted development with no quality bar — and agentic engineering, a professional discipline of managing fallible agents as powerful but unpredictable collaborators. The distinction: "vibe coding raises the floor, agentic engineering raises the ceiling." A December 2025 reliability inflection point, where larger code chunks began consistently landing correct without correction, made agentic engineering viable as a daily practice rather than an occasional experiment.

## Key Concepts

- Vibe coding has no quality bar; code runs but the product can still break, illustrated by a case of cross-matching different email systems (Stripe versus Google) that silently corrupted user credits.
- Agentic engineering names five core skills: spec design, diff review, eval design, security oversight, and quality taste.
- The December 2025 inflection point shifted programming from writing lines of code to delegating macro actions — implement a feature, refactor a subsystem, compare approaches.
- As agents absorb generation, human skills that grow scarcer and more valuable are understanding, taste, system-design judgment, eval design, and agent orchestration.

## Terminology

- Vibe coding — low-friction, low-oversight AI-assisted code generation, accepted and shipped without rigorous review.
- Agentic engineering — the professional orchestration of AI agents through rigorous specification, review, and evaluation discipline.
- Diff review — reading generated code for architectural soundness and cross-system assumptions, not merely syntactic correctness.
- Eval design — building measurable feedback loops with verifiable signals so an agent's output can be judged and improved.

## Architecture and Implementation

Karpathy's proposed upgrade path has four steps: slow down at the spec stage, since twenty minutes of specification saves hours of bad diffs; review every diff for architecture, not syntax; build feedback loops with verifiable signals (tests, evals, benchmarks); and maintain conceptual ownership of the fundamentals an agent gets wrong under pressure. His proposed hiring test replaces small puzzle interviews with a substantial project deployment under adversarial testing, scored on whether a candidate can decompose work for agents, write a useful and detailed specification, preserve quality while moving fast, review generated work rigorously, and secure and harden the result.

## Code Examples

None. The lesson is a conceptual and hiring-practice commentary, not a code walkthrough.

## Best Practices

- Write specifications, including invariants and security boundaries, before prompting an agent.
- Review every diff for architectural soundness and cross-system assumptions, not just whether it runs.
- Build verifiable feedback loops — tests, evals, benchmarks — so agent output can be judged, not just accepted.
- Retain conceptual ownership of fundamentals; do not outsource comprehension along with generation.

## Warnings and Anti-Patterns

- Accepting generated code without architectural review introduces vulnerabilities the model cannot see for itself.
- Agents make plausible-but-wrong system-design decisions, such as using an unstable identifier like email across systems that treat it differently.
- Code that "works" can still be bloated, copy-pasted, or poorly abstracted; a passing test is not a quality bar.

## Related Concepts

- [[best-practices-index]]
- [[evaluation]]
- [[what-is-an-ai-agent]]
- [[20_People/andrej-karpathy/profile|Andrej Karpathy]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The commentary does not cite Karpathy's original transcript or slides directly; a future research pass should source the Sequoia Ascent talk itself rather than this secondary summary.

## References

- Agentic Engineering: Karpathy's New Framework — https://www.aibuilderclub.com/blog/karpathy-agentic-engineering
