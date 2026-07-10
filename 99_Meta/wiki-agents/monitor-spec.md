---
type: meta
title: Monitor Specification
status: permanent
created: 2026-07-10
topic:
- topic/meta
tags:
- wiki-agents
---

# Monitor Specification

This file specifies the background monitor that populates the vault from the
watchlist. The monitor is self-contained. It does not depend on the
thinkers-coupled plan scripts. A later pass registers it as an executable
subagent; this pass defines its contract.

## Purpose

For one channel slug, plan queries against the channel surface, fetch sources
published since the last run, write one source note per accepted candidate, and
update the channel state.

## Inputs

| Input | Source |
|---|---|
| channel slug | invocation argument |
| channel surface | `watchlist.md` surface notes |
| last run time | `state/<channel>.json` field `last_run_at` |
| per-run ceiling | `watchlist.md` field `target_per_run` |
| query plan | `queries/<channel>.md` |

## Procedure

1. Read the channel row from `watchlist.md` and the state file.
2. Plan queries from `queries/<channel>.md`.
3. Fetch candidates published after `last_run_at`.
4. Filter for primary sources. Reject low-quality opinion pieces.
5. For each accepted candidate, write a source note under
   `10_Sources/<Category>/` from `90_Templates/template - source.md`. Set
   `watchlist_channel` to the slug. Set `anthropic: true` for Anthropic material.
6. Extract structured knowledge: summary, key concepts, terminology,
   architecture, code, best practices, warnings, related concepts, references.
7. Link each source note to at least one concept, person, or organisation.
8. Update `state/<channel>.json`: `last_run_at`, `sources_added`, `last_status`.

## Stop conditions

- The run reaches `target_per_run`.
- Three consecutive query rounds return nothing new.

## Output contract

Each run appends a one-line result to the state file history: run time, count
added, and status. The monitor never edits notes outside `10_Sources/` and its
own state.

## State file schema

```json
{
  "channel": "anthropic-news",
  "last_run_at": "2026-07-10T00:00:00Z",
  "target_per_run": 5,
  "sources_added": 0,
  "last_status": "pending",
  "history": []
}
```
