---
type: meta
title: Workflow — Release-Note Ingestion
aliases:
- "Workflow — Release-Note Ingestion"
status: permanent
created: 2026-07-10
topic:
- topic/meta
tags:
- wiki-agents
- workflow
---

# Workflow — Release-Note Ingestion

The loop that records each Anthropic release chronologically.

## Trigger

An Anthropic release: a model, a Claude Code version, an SDK milestone, or an
MCP update.

## Steps

1. Create a note under `10_Sources/Release-Notes/` named
   `<product>-<yyyy-mm-dd>.md` from `90_Templates/template - release-note.md`.
2. Fill: summary, new capabilities, deprecated features, migration notes,
   engineering implications, practical examples.
3. Set `anthropic: true` and `topic: [topic/release-notes]`.
4. Link engineering implications to affected concept notes, for example
   [[mcp]], [[claude-agent-sdk]], or [[claude-code]].
5. Add the note to `[[MOC - Release Notes]]`.
6. Where the release changes a documented behaviour, update the affected note
   and its `updated` stamp.

## Verification

- The release note cites the canonical release URL and changelog.
- `[[MOC - Release Notes]]` lists the new note.

## Related

- [[Workflow — Weekly Maintenance]]
- [[99_Meta/roadmap.md|Roadmap]]
