---
type: meta
title: Recommended Plugins
status: permanent
created: 2026-07-10
topic:
- topic/meta
tags: []
---

# Recommended Plugins

The vault depends on four community plugins. Each earns its place.

| Plugin | Purpose | Why it matters here |
|---|---|---|
| Dataview | Queries frontmatter into live lists and tables. | Every MOC lists its topic's notes without hand-maintenance. The vault dashboard tracks stubs and orphans. |
| Tasks | Query-driven task management over checkboxes. | The weekly-maintenance loop tracks as queryable tasks. |
| Templater | Applies the templates in `90_Templates/`. | New notes inherit the correct frontmatter and body skeleton. |
| Obsidian Git | Commits and pushes the vault on a schedule. | The vault is a git repo; version history protects the knowledge base. |

## Install order

1. Dataview. Enable JavaScript queries off by default; the MOCs use plain
   Dataview list syntax.
2. Templater. Point the template folder at `90_Templates/`.
3. Tasks.
4. Obsidian Git.

## Dataview settings

- Enable "Automatic View Refresh".
- Leave "Enable Inline JS Queries" off. The vault avoids JS queries for safety.

## Core plugins

Enable the built-in Graph View, Backlinks, Outgoing Links, and Outline.
