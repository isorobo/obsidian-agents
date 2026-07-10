---
type: meta
title: NotebookLM Bridge
status: permanent
created: 2026-07-10
topic:
- topic/meta
tags: []
---

# NotebookLM Bridge

NotebookLM is the primary research corpus for authoritative material. This file
states the round-trip contract between vault source notes and NotebookLM
sources.

## Corpus scope

Collect primary sources only:

- Anthropic documentation, engineering blog, news, and release notes.
- Anthropic GitHub repositories and SDK references.
- Conference talks and recorded presentations by named speakers.
- Research papers and technical whitepapers.
- API and MCP references.

Exclude low-quality opinion pieces. Prioritise primary sources.

## Round-trip contract

| Direction | Mechanism |
|---|---|
| Vault to NotebookLM | A source note with `nlm_skip: false` pushes to the notebook. The returned source UUID writes back to `nlm_id`. |
| NotebookLM to vault | Briefs, audio, and slides download to `10_Sources/NotebookLM-Exports/`. Each export back-links to its source note. |

## Field dependencies

- `nlm_id` maps a vault source note to a NotebookLM source.
- `nlm_skip` excludes a source from export.
- `nlm_last_sync` stamps the last round-trip.

## Ingestion workflow

1. Triage new sources in `00_Inbox/`.
2. Push accepted sources to the notebook. Record `nlm_id`.
3. Generate a brief or audio overview per theme.
4. Download exports to `10_Sources/NotebookLM-Exports/`.
5. Extract structured knowledge into concept and guide notes.
6. Back-link every export to its source and concept notes.

## Knowledge extraction target

Every source converts into structured knowledge: summary, key concepts,
terminology, architecture, implementation guidance, code examples, best
practices, warnings, anti-patterns, related concepts, future work, references.
