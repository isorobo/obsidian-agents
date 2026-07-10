---
type: meta
title: Workflow — Weekly Maintenance
aliases:
- "Workflow — Weekly Maintenance"
status: permanent
created: 2026-07-10
topic:
- topic/meta
tags:
- wiki-agents
- workflow
---

# Workflow — Weekly Maintenance

A weekly loop that runs every active channel and keeps the graph healthy.

## Steps

- [ ] Run every `active` channel in `watchlist.md`.
- [ ] Refresh each MOC. Confirm the Dataview query lists new notes.
- [ ] Check for orphans. Resolve any note with zero links.
- [ ] Check for broken wikilinks. Fix or create the target.
- [ ] Promote stubs. Move enriched notes from `stub` to `draft` or `review`.
- [ ] Update `[[99_Meta/roadmap.md|the roadmap]]` milestone state.
- [ ] Commit the vault through Obsidian Git.

## Verification

- Orphan count on the dashboard reads zero for permanent notes.
- The graph view shows one connected cluster.

## Related

- [[Workflow — Daily Research]]
- [[Workflow — Release-Note Ingestion]]
- [[Workflow — NotebookLM Ingestion]]
