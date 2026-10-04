# Query plan - anthropic-engineering

Base surface: see `watchlist.md` channel surface notes.

## Window
- since_date: 2024-01-01 (low-volume blog; take the back catalogue over several runs)

## Fetch method
- WebFetch `https://www.anthropic.com/engineering`; fallback: `/engineering/` URLs from `https://www.anthropic.com/sitemap.xml`, then WebSearch `site:anthropic.com/engineering`.

## Include filters
- every post on the Anthropic Engineering blog (the channel takes all posts)
- in particular: building agents, multi-agent systems, tool design, context engineering, evaluations, Claude Code practice, Agent SDK, MCP, sandboxing and security of agents

## Exclude filters
- posts outside `anthropic.com/engineering` (news posts belong to anthropic-news)
- duplicates of existing source notes (two posts are already in the vault: building effective agents, demystifying evals)

## Priority
1. Newest unseen posts
2. Older unseen posts, newest first
