# Query plan - anthropic-news

Base surface: see `watchlist.md` channel surface notes.

## Window
- since_date: 2026-06-01 (the vault's one existing release note is dated 2026-06-30)

## Fetch method
- WebFetch `https://www.anthropic.com/news`; if the listing is empty or rendered client-side, take `/news/` URLs from `https://www.anthropic.com/sitemap.xml`, else WebSearch `site:anthropic.com/news`.
- Release items go to `10_Sources/Release-Notes/` (release template). Non-release posts with agent-engineering guidance go to `10_Sources/Blog/` (source template, `source_type: blog`).

## Include filters
- model releases (new Claude models, versions, availability, pricing or context changes that affect agents)
- Claude Code releases, milestones and features
- Claude API and Claude Agent SDK launches (tools, skills, memory, context management, files, batch, caching)
- MCP announcements and Anthropic's MCP connector updates
- agent guidance posts (building agents, context engineering, evaluation, safety of agent deployments)

## Exclude filters
- policy, economic, societal impact and research-only interpretability posts with no agent-engineering content
- company news: funding, hiring, offices, partnerships and customer stories
- low-quality opinion pieces
- duplicates of existing source notes

## Priority
1. Model and Claude Code releases
2. API and SDK launches, MCP updates
3. Agent guidance posts
