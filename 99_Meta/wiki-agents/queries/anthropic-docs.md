# Query plan - anthropic-docs

Base surface: see `watchlist.md` channel surface notes.

## Window
- since_date: 2024-01-01 (documentation pages are often undated; dedupe governs)

## Fetch method
- `docs.anthropic.com` redirects; resolve it and record the resolved host in the run summary.
- Page index: WebFetch `https://docs.claude.com/llms.txt` (API, agents and tools) and `https://code.claude.com/docs/llms.txt` (Claude Code, Agent SDK); fallback to each host's `sitemap.xml`.

## Include filters
- agents and tools: tool use, tool definitions, computer use, web search and fetch tools, code execution, memory tool, context editing
- MCP: MCP connector, remote MCP servers, MCP in Claude Code
- Agent Skills: authoring, packaging, using skills in the API and in Claude Code
- Claude Agent SDK: overview, sessions, permissions, hooks, subagents, cost tracking, hosting
- Claude Code: headless and print mode, settings and permissions, hooks, subagents, slash commands, plugins, security
- pages new to the vault; a revised page already in the vault is reported as a revision candidate, not re-ingested

## Exclude filters
- marketing landing pages, pricing tables, release-note index pages (releases belong to anthropic-news and claude-code-changelog)
- per-language SDK reference stubs with no explanatory text
- duplicates of existing source notes

## Priority
1. Claude Code headless, permissions and hooks pages (they bear on the code-factory adapter)
2. Agent SDK and tool-use pages
3. MCP and Agent Skills pages
