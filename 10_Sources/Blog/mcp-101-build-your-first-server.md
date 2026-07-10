---
type: source
status: draft
created: 2026-07-11
title: "MCP 101: Build Your First MCP Server (Step-by-Step)"
authors:
- AI Builder Club
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 3.1
url: https://www.aibuilderclub.com/blog/mcp-101-build-mcp-servers
year: 2026
date_published: 2026-04-16
anthropic: false
topic:
- topic/mcp
tags:
- mcp
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
---

# MCP 101: Build Your First MCP Server (Step-by-Step)

> AI Builder Club, "MCP 101: Build Your First MCP Server (Step-by-Step)", Build AI Agents Course, 16 April 2026 (updated 7 May 2026), https://www.aibuilderclub.com/blog/mcp-101-build-mcp-servers.

## Summary

Chapter 3 opens with the standardisation problem MCP solves: before it, every AI client needed its own integration with every tool provider. MCP gives clients and servers one shared protocol — the lesson's own metaphor is "USB-C for AI tools" — built from three component types (Tools, Resources, Prompts) communicating over JSON-RPC. The lesson walks a complete, roughly 60-line Python weather server from first line to a working connection in Claude Desktop and Cursor.

## Key Concepts

- MCP has three primitives: Tools (actions the model can invoke, the most commonly used), Resources (read-only data exposed as virtual files), and Prompts (named, reusable prompt templates).
- Architecture is client, server, and transport: stdio for local servers, HTTP/SSE for remote ones, both carrying JSON-RPC messages.
- Function calling and MCP solve related but different problems: a hand-written function-calling tool works with one API only, while an MCP server works with any MCP client without modification.
- Claude Code can generate a working MCP server from a natural-language description, which the lesson says cuts initial build time from roughly an hour to under ten minutes.

## Terminology

- MCP server — a lightweight local or remote process that exposes Tools, Resources, and Prompts to any MCP-speaking client over JSON-RPC.
- Transport — the communication channel between client and server: stdio for local processes, HTTP/SSE for remote ones.

## Architecture and Implementation

The reference server (`Server("weather-server")`) registers a `get_weather` tool via `@app.list_tools()` and `@app.call_tool()` decorators, fetches data from the free wttr.in API with a 10-second timeout, and raises `ValueError` on an unrecognised tool name, all run over `stdio_server()`. Connecting it to Claude Desktop or Cursor is a JSON configuration edit naming the launch command and file path, after which the server's tools appear in the client automatically.

## Code Examples

A complete roughly-60-line weather MCP server (tool declaration, tool execution, stdio transport, timeout and error handling), plus the Claude Desktop and Cursor configuration snippets needed to connect it.

## Best Practices

- Scope each server's credentials to the minimum permission it needs; do not share one broad API key across servers.
- Install MCP servers only from sources you trust; review tool descriptions before enabling a server, since those descriptions are what the model actually reads.
- Start with stdio for local development before moving to HTTP/SSE for a remote deployment.

## Warnings and Anti-Patterns

- An MCP server runs with the permissions of the process that launches it — trust in the server is trust in arbitrary local code execution, not a sandboxed capability grant.
- Skipping a read of the actual tool descriptions before enabling a server means accepting instructions you have not reviewed, since the model reads them even if you do not.

## Related Concepts

- [[mcp]]
- [[tool-use]]
- [[claude-code]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson points forward to its own security and internals follow-ups (3.2, 3.3) and to the official `modelcontextprotocol/servers` repository for production-ready Filesystem, GitHub, Postgres, Brave Search, Slack, and Google Maps servers.

## References

- MCP 101: Build Your First MCP Server (Step-by-Step) — https://www.aibuilderclub.com/blog/mcp-101-build-mcp-servers
