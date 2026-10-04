# Query plan - anthropic-github

Base surface: see `watchlist.md` channel surface notes.

## Window
- since_date: 2026-01-01

## Fetch method
- WebFetch `https://api.github.com/orgs/anthropics/repos?per_page=100&sort=pushed`; for in-scope repos `https://api.github.com/repos/anthropics/<repo>/releases?per_page=10` and `https://raw.githubusercontent.com/anthropics/<repo>/HEAD/README.md` (unauthenticated, rate-limited; `gh` is not available in headless runs).

## Include filters
- Claude Agent SDK repositories (Python and TypeScript): README and minor or major releases
- Anthropic API SDK repositories: releases that add agent features (tool runner, MCP helpers, memory, skills)
- Claude Code adjacent repositories (for example the GitHub Action, devcontainer, plugin or skills repositories): README and significant releases
- MCP-related repositories in the anthropics organisation
- new public repositories in the organisation that are about agents

## Exclude filters
- Claude Code version releases (they belong to claude-code-changelog)
- patch releases with only bug fixes and no behaviour change
- archived repositories, forks, demos with no README content, quickstart apps
- duplicates of existing source notes

## Priority
1. Agent SDK releases with behaviour change
2. New agent-related repositories
3. Significant releases elsewhere
