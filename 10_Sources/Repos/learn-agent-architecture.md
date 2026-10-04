---
type: source
status: draft
created: 2026-10-04
title: "learn-agent-architecture"
authors:
- hardness1020
organisation: hardness1020
source_type: repo
venue: GitHub
url: https://github.com/hardness1020/learn-agent-architecture
year: 2026
date_published: 2026-06-23
anthropic: false
topic:
- topic/architectures
- topic/foundations
tags:
- agent-harness
- agent-loop
- learning-resource
- implementation-comparison
nlm_id:
nlm_skip: false
watchlist_channel: af-corpus-repos
af_targets:
- af:RSCH-01/learn-agent-architecture
- af:ADR-0001
- af:RSCH-04/Q03
- af:RSCH-04/Q30
- af:RSCH-04/Q31
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: d16ab18bf5d26fe9ba03de527da1d047b8d3a9ce1bdca431076ed82e492b6dfb
---

# learn-agent-architecture

> hardness1020, "learn-agent-architecture", GitHub, 23 June 2026, https://github.com/hardness1020/learn-agent-architecture.

## Summary

The repository teaches how modern agents are built, centred on the harness: the engineering layer that turns model reasoning into controlled action by running tools, keeping state across calls, gating side effects and coordinating loops. Its README states the thesis as "The model reasons. The harness turns that reasoning into controlled action." It holds 24 self-contained sections in eight layers, from foundations through the core loop, complex work, memory and resilience, long-running tasks, multi-agent coordination, extension and observability, to composition (loop and graph engineering). Each section follows one lens: opening problem, mechanism, per-system implementation, failure modes. It was created 23 June 2026, last pushed 23 September 2026, MIT licence (GitHub API, this run). This is an overview from the README only; chapters were not read.

## Key Concepts

- Agency emerges from the harness, not the model alone.
- One shared control flow underlies coding tools, chat assistants and autonomous runners.
- Memory, skills and context management enable long-horizon work.
- Graph engineering moves control flow from model decisions to coded edges.

## Terminology

- Harness: the code around the model that runs tools, holds state and gates effects.
- Layer: one of the eight groupings of sections.

## Architecture and Implementation

Four systems serve as case studies: Claude Code (all sections), Hermes Agent (memory and long-term assistance), mini-swe-agent (a minimal loop baseline of about 150 lines) and a DeepSeek harness (plugin-first). Readers study source diffs between adjacent sections to isolate one mechanism at a time. Each section ships an offline `test.py` and a live `demo.py`.

## Code Examples

```bash
uv venv
uv pip install -r requirements.txt
cp .env.example .env  # add ANTHROPIC_API_KEY
```

## Best Practices

- Learn one mechanism at a time by diffing adjacent sections.
- Run the offline test before the live demo.

## Warnings and Anti-Patterns

The README carries no explicit warnings section; failure modes are covered per chapter.

## Related Concepts

- [[the-agent-loop]]
- [[claude-code]]
- [[tool-use]]
- [[memory]]

## Future Work

Chapter-level notes on permissions, subagents, sessions and recovery are candidates for later runs.

## References

- https://github.com/hardness1020/learn-agent-architecture
