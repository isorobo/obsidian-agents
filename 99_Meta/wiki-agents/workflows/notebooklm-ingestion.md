---
type: meta
title: Workflow — NotebookLM Ingestion
aliases:
- "Workflow — NotebookLM Ingestion"
status: permanent
created: 2026-07-10
topic:
- topic/meta
tags:
- wiki-agents
- workflow
---

# Workflow — NotebookLM Ingestion

The loop that treats NotebookLM as the primary research corpus. See
[[99_Meta/NotebookLM-bridge.md|the NotebookLM bridge]] for the field contract.

## Steps

1. Select source notes with `nlm_skip: false` awaiting sync.
2. Push each to the NotebookLM notebook. Record the returned UUID in `nlm_id`.
3. Generate a brief or audio overview per theme.
4. Download exports to `10_Sources/NotebookLM-Exports/`.
5. Extract structured knowledge into concept and guide notes.
6. Back-link every export to its source and concept notes.
7. Stamp `nlm_last_sync` on each synced note.

## Corpus rule

Collect primary sources: Anthropic material, GitHub, official documentation,
research papers, conference talks. Reject low-quality opinion pieces.

## Verification

- Each export back-links to a source note.
- `nlm_id` resolves on every synced source.

## Related

- [[99_Meta/NotebookLM-bridge.md|NotebookLM Bridge]]
- [[Workflow — Weekly Maintenance]]
