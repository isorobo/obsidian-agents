---
type: source
status: draft
created: 2026-10-04
title: "The 6 Components of a Production Agent Harness"
authors:
- Shirley
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club - Build AI Agents Course
url: https://www.aibuilderclub.com/blog/harness-six-components
year: 2026
date_published: 2026-06-11
anthropic: false
topic:
- topic/architectures
- topic/observability
tags:
- harness
- agent-architecture
- production
- recovery
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
af_targets:
- af:ADR-0002
- af:ADR-0005
- af:ADR-0008
- af:RSCH-04/Q03
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: d6df4f121a53c4fdf7a967f1b1548a11670b491484ac0af70880eb8eb70a49ec
---

# The 6 Components of a Production Agent Harness

> Shirley, "The 6 Components of a Production Agent Harness", AI Builder Club, Build AI Agents Course, 11 June 2026 (updated 2 July 2026), https://www.aibuilderclub.com/blog/harness-six-components.

## Summary

The lesson states Agent = Model + Harness, where the harness is everything around the model that makes it production-grade. It names six components: context management, tool system, orchestration, state and memory, evaluation and observability, and constraints and recovery. Each has a named failure when missing. The author's claim is that most builders do tools well and neglect evaluation and recovery, which is the gap between a demo and production.

## Key Concepts

- Context management: what the model perceives. Missing, quality is inconsistent and constraints are forgotten.
- Tool system: what the agent can reach. Missing calibration, it picks wrong tools or hallucinates facts.
- Orchestration: sequencing and decision points.
- State and memory: persistence across runs.
- Evaluation and observability: correctness checks and debuggability.
- Constraints and recovery: boundaries, and containing a single failure.
- Diagnosis works backwards: read the failure pattern to find the weak component.

## Terminology

- Tool calibration: balancing tool availability against selection accuracy.
- Run state: position within one task, distinct from session memory and long-term memory.
- Hard rails: constraints that hold regardless of model preference.
- Generator/evaluator pattern: separate production and acceptance agents.

## Architecture and Implementation

The harness is described as load-bearing walls around the model. The lesson keeps three kinds of state apart (run state, session memory, long-term memory) and scopes toolsets to a job rather than a universal menu.

## Code Examples

The source carries no reusable code in the portions fetched.

## Best Practices

- Scope tools to the job domain.
- Record structured traces of intermediate steps.
- Use a fresh-context evaluator, not self-grading.
- Keep failure evidence in context during recovery.
- Define termination conditions and escalation rules explicitly.

## Warnings and Anti-Patterns

- Dumping raw search results into context without distillation.
- Conflating run state, session memory and long-term memory.
- Skipping evaluation layers.
- Treating a role label as a sandbox.
- Mixing expired facts with current working memory.

## Related Concepts

- [[the-agent-loop]]
- [[memory]]
- [[evaluation]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson points to companion pieces on harness practice at OpenAI and Anthropic and on loop engineering.

## References

- The 6 Components of a Production Agent Harness: https://www.aibuilderclub.com/blog/harness-six-components
- Cited by the lesson: LangChain, "The Anatomy of an Agent Harness"; OpenAI, "Harness Engineering: Leveraging Codex in an Agent-First World"; Anthropic, "Harness Design for Long-Running Application Development".
