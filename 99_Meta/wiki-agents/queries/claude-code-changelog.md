# Query plan - claude-code-changelog

Base surface: see `watchlist.md` channel surface notes.

## Window
- since_date: set on the first run to the date of the oldest of the newest `target_per_run` versions (no older backfill)

## Fetch method
- WebFetch `https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md`; split on version headings.
- Release dates: WebFetch `https://api.github.com/repos/anthropics/claude-code/releases?per_page=30` (`published_at`), else the npm registry `https://registry.npmjs.org/@anthropic-ai/claude-code` (`time[<version>]`).
- One release note per version: `10_Sources/Release-Notes/claude-code-<version with hyphens>-<yyyy-mm-dd>.md`, `product: Claude Code`, `version: <x.y.z>`.
- `url` per note must be unique: the GitHub release page `https://github.com/anthropics/claude-code/releases/tag/v<version>` when it exists, else `https://www.npmjs.com/package/@anthropic-ai/claude-code/v/<version>`. Never the bare CHANGELOG URL (every version would share it).

## Include filters
- every version heading in the changelog (each version is recorded as a release note)
- in Engineering Implications, call out changes to: print and headless mode (`-p`), output formats (stream-json), tool and permission flags, settings sources, MCP configuration, hooks, subagents, skills, plugins, authentication and login behaviour, model selection

## Exclude filters
- versions already recorded
- duplicates of existing source notes

## Priority
1. Unseen versions in ascending version order from the window floor
2. If more than `target_per_run` are unseen, record the oldest first and flag the backlog
