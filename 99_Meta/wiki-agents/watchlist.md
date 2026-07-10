---
type: meta
title: wiki-agents Channel Watchlist
status: permanent
created: 2026-07-10
topic:
- topic/meta
tags:
- monitor-config
- wiki-agents
---

# Watchlist

Living watchlist of source channels the research pipeline runs on each refresh.
The monitor reads this table on every `run all` and `weekly-refresh`.

## Conventions

- `channel` — slug used in `state/<channel>.json` and `queries/<channel>.md`.
- `name` — display name.
- `category` — matches the destination folder under `10_Sources/`.
- `cadence` — expected publication frequency.
- `target_per_run` — ceiling on sources added per run. The monitor exits earlier
  when the channel is dry.
- `status` — `pilot`, `active`, `paused`, or `pending`.

## Table

| channel | name | category | cadence | target_per_run | status |
|---|---|---|---|---|---|
| anthropic-news | Anthropic News and Release Notes | Release-Notes | weekly | 5 | pilot |
| anthropic-engineering | Anthropic Engineering Blog | Blog | weekly | 5 | active |
| anthropic-docs | Anthropic Documentation | Docs | irregular | 5 | active |
| anthropic-github | anthropics GitHub org | Repos | weekly | 6 | active |
| claude-code-changelog | Claude Code Changelog | Release-Notes | weekly | 5 | active |
| arxiv-agents | arXiv cs.AI and cs.MA agent tags | Papers | weekly | 6 | active |
| boris-cherny | Boris Cherny talks, posts, interviews | Talks | irregular | 3 | active |

## Promote to active

The pilot **anthropic-news** runs first to validate the end-to-end loop. Once it
ships one clean cycle, promote `anthropic-engineering` and `anthropic-docs`.

## Channel surface notes

- **anthropic-news** — base URL: `https://www.anthropic.com/news`. Filter titles
  for model releases, Claude Code, SDK, MCP, and agent guidance.
- **anthropic-engineering** — base URL: `https://www.anthropic.com/engineering`.
  Take every post; the blog is high-signal and low-volume.
- **anthropic-docs** — base URL: `https://docs.anthropic.com`. Watch the
  agents-and-tools, MCP, and SDK sections for new or revised pages.
- **anthropic-github** — base URL: `https://github.com/orgs/anthropics/repositories`.
  Watch releases and READMEs on SDK, Claude Code, and MCP repositories.
- **claude-code-changelog** — the Claude Code CHANGELOG. Record each version as a
  release note.
- **arxiv-agents** — arXiv `cs.AI` and `cs.MA`. Filter titles and abstracts for
  `agent`, `tool use`, `planning`, `multi-agent`, `reflexion`, `ReAct`.
- **boris-cherny** — talks, interviews, and posts where Boris Cherny is a named
  speaker or author. Extract engineering principles, not only links.
