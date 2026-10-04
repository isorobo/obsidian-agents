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
| aibuilderclub | AI Builder Club — Build AI Agents Course and blog | Blog | irregular | 5 | active |
| af-corpus-repos | Agent-factory corpus repositories (12-Factor Agents, learn-agent-architecture, mini-SWE-agent, smolagents) | Repos | irregular | 4 | active |
| af-corpus-papers | Agent-factory corpus papers (Generative Agents and agent-architecture papers) | Papers | irregular | 3 | active |

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
- **aibuilderclub** — base URL: `https://www.aibuilderclub.com/blog`. Publisher
  of the numbered "Build AI Agents Course" (Chapter 1 seeded 2026-07-11, lessons
  1.2–1.12) plus a running blog. Includes AI Builder Club's own commentary on
  Andrej Karpathy's public talks and posts — tag those `topic/karpathy` in
  addition to their general topic, per `99_Meta/schema.md` section 2.3. Watch
  for new numbered chapters and standalone posts; skip video-only lessons with
  no companion article.
- **af-corpus-repos** - the four repositories in agent-factory's RSCH-01 research
  corpus, and nothing else: `https://github.com/humanlayer/12-factor-agents`,
  `https://github.com/hardness1020/learn-agent-architecture`,
  `https://github.com/SWE-agent/mini-swe-agent`, and
  `https://github.com/huggingface/smolagents`. Watch the README, the docs and
  content folders inside each repository, and releases. Every note is a
  `source_type: repo` note whose `url` points into one of the four repositories.
  First pass: one overview note per repository. Then the docs parts that explain
  the loop, tools, state, memory, context, delegation, permissions, recovery and
  evaluation, then releases that change the architecture. Set `af_targets` with
  the matching `af:RSCH-01/<item>` ID.
- **af-corpus-papers** - papers for agent-factory's RSCH-01 corpus and its 33
  research questions (RSCH-04). Start with Generative Agents (Park et al. 2023,
  arXiv 2304.03442), then the numbered seed list in `queries/af-corpus-papers.md`,
  then arXiv searches on the plan's question keywords. Papers already in the vault
  (ReAct, Reflexion, Voyager, AutoGen, CAMEL, AgentVerse and the surveys) are
  duplicates. Tag `topic/research-papers` plus a general topic.

## State reconciliation (2026-10-04)

This table is authoritative for `target_per_run`. On 2026-10-04 three state files
disagreed with it: `anthropic-github` (state 5, table 6), `arxiv-agents` (state 5,
table 6) and `boris-cherny` (state 5, table 3). `/wiki-agents init` runs
`wiki_vault.py reconcile --write` for every channel, which copies the table value
into state, extends each state file to the monitor schema (dedupe arrays, rejected
list, dry-round counter, run summary), and sets the source count from disk. The
first-run date floor for each channel (`since_date`) comes from the `## Window`
section of its query plan.

The pilot gate stays in force: until `anthropic-news` has one clean automated run,
`run all` runs only the pilot, unless it is called with `--all` (authorised for the
rebuild). Naming a channel (`run <channel>`) runs it regardless.

The two `af-corpus-*` channels feed the agent-factory digest in
`99_Meta/agent-factory-digest/`. The feed is one way: agent-factory never reads
this vault.
