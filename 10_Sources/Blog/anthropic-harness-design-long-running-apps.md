---
type: source
status: draft
created: 2026-10-04
title: "Harness design for long-running application development"
authors:
- Prithvi Rajasekaran
organisation: Anthropic
source_type: blog
venue: Anthropic Engineering
url: https://www.anthropic.com/engineering/harness-design-long-running-apps
year: 2026
date_published: 2026-03-24
anthropic: true
topic:
- topic/multi-agent
- topic/architectures
- topic/evaluation
tags:
- harness
- planner-generator-evaluator
- context-reset
- long-running-agents
- sprint-contracts
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-engineering
af_targets:
- af:DELEG-03
- af:ADR-0008
- af:RSCH-04/Q18
- af:RSCH-04/Q12
- af:DELEG-01
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 54f745423c2fef415e6ddd60b29c8f6d894568119ce0cce65d1b25b3a3edcbe1
---

# Harness design for long-running application development

> Prithvi Rajasekaran, "Harness design for long-running application development", Anthropic Engineering (Anthropic Labs), 24 March 2026, https://www.anthropic.com/engineering/harness-design-long-running-apps.

## Summary

The post describes a three-role harness for building full applications over hours: a planner that expands a brief prompt into a product spec, a generator that implements features, and an evaluator that tests with Playwright and grades against criteria. The design is GAN-inspired: separating generation from evaluation counters the tendency of models to praise their own work. In a retro game maker example a solo agent (20 minutes, $9) produced broken core functionality, while the full harness (6 hours, $200) produced a polished, working result. With Opus 4.6 the sprint decomposition was removed, a DAW example ran 3 hours 50 minutes for $124.70, and the evaluator still caught real gaps.

## Key Concepts

- Self-evaluation bias: models rate their own mediocre output highly.
- Context anxiety: models wrap up early as they sense the context limit; resets worked better than compaction for Opus 4.5, and Opus 4.6 removed the behaviour.
- Sprint contracts: generator and evaluator agree testable success criteria before building.
- Gradable criteria for subjective work: design quality, originality, craft and functionality.

## Terminology

- Harness: the orchestrating scaffold around the agents.
- Load-bearing component: a harness piece that measurably improves results.

## Architecture and Implementation

Agents hand off through files. The generator works with git, the evaluator drives the app through Playwright MCP, and orchestration uses the Claude Agent SDK. The sample stack was React, Vite and FastAPI with SQLite or PostgreSQL.

## Code Examples

The source carries no reusable code.

## Best Practices

- Strip harness parts iteratively and test what the model can now do alone.
- Tune the evaluator to be sceptical using few-shot examples.
- Re-examine the harness with each new model release.
- Use file-based handoffs for structure.

## Warnings and Anti-Patterns

- Trusting an agent to grade its own work.
- Letting context fill on long tasks without a reset strategy.
- Under-scoped work without an upfront spec.
- Superficial evaluator testing that misses edge cases.

## Related Concepts

- [[supervisor-worker-multi-agent]]
- [[claude-agent-sdk]]
- [[evaluation]]
- [[plan-and-execute]]

## Future Work

The author expects harness components to keep shrinking or shifting as models improve.

## References

- https://www.anthropic.com/engineering/harness-design-long-running-apps
