---
type: meta
title: wiki-agents Pipeline — Index
status: permanent
created: 2026-07-10
topic:
- topic/meta
tags:
- wiki-agents
---

# wiki-agents Pipeline — Index

The research pipeline that grows the vault. Self-contained; independent of the
sibling thinkers and tokenise scripts.

## Components

| File | Role |
|---|---|
| [[watchlist]] | Channel table the monitor reads each run. |
| [[monitor-spec]] | The monitor contract: inputs, procedure, stop conditions. |
| `state/<channel>.json` | Per-channel run state. |
| `queries/<channel>.md` | Per-channel query plan. |

## Workflows

- [[Workflow — Daily Research]]
- [[Workflow — Weekly Maintenance]]
- [[Workflow — Release-Note Ingestion]]
- [[Workflow — NotebookLM Ingestion]]

## Bridges

- [[99_Meta/NotebookLM-bridge.md|NotebookLM Bridge]]

## Governance

- Schema: [[99_Meta/schema.md|schema]]
- Roadmap: [[99_Meta/roadmap.md|roadmap]]
- Design of record: [[99_Meta/design/2026-07-10-wiki-agents-foundation-design.md|design spec]]
