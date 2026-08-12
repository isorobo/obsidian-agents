---
type: source
status: draft
created: 2026-08-13
title: "The Complete Guide to MCP Servers: What They Are and How to Build One"
authors: []
organisation: Claude Code Playbooks
source_type: blog
venue: Claude Code Playbooks Blog
url: TBD
year: 2026
date_published: 2026-04-16
anthropic: false
topic:
- topic/mcp
- topic/best-practices
tags: [mcp, fastmcp, stdio, tool-design, claude-code-playbooks]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
---

# The Complete Guide to MCP Servers: What They Are and How to Build One

> Claude Code Playbooks, "The Complete Guide to MCP Servers: What They Are and
> How to Build One", Claude Code Playbooks Blog, MCP category, Intermediate
> level, 16 April 2026. URL TBD.

## Summary

The post defines MCP, argues its value, then walks a build from install to
running server. Much of the ground is covered in the vault. The USB-C
comparison, the three primitives, the JSON-RPC handshake, and the stdio
against HTTP split all appear in
[[10_Sources/Docs/mcp-introduction|What is MCP?]],
[[10_Sources/Blog/mcp-101-build-your-first-server|MCP 101]], and
[[10_Sources/Blog/mcp-internals-client-server|MCP Internals]]. Three parts add
new material. First, five design principles for a tool surface, written from
the model's point of view. Second, a decision rule for choosing a remote server
over a local one, with three named triggers. Third, a FastMCP walkthrough that
registers a tool, a resource, and a prompt through decorators, where MCP 101
uses the lower-level `Server` API. The site footer reads "Built for the Claude
Code community. Not affiliated with Anthropic", so `anthropic` is false.

## Key Concepts

- MCP is a specification, not a framework, a service, or a library.
- A server exposes three kinds of thing: tools, resources, and prompts.
- Decoupling the model from its tools produces three effects: portable
  integrations, composable capabilities, and a compounding ecosystem.
- One agent connects to several servers at once and reasons across them.
- The handshake runs in three phases: initialize, discovery, and invocation.
- Local servers run as subprocesses over stdio. Remote servers run over HTTP
  with Server-Sent Events.

## Terminology

- Tool: a function the agent calls, with a name, a JSON Schema for inputs, and
  a return type.
- Resource: read-only data addressed by URI that the agent pulls into context.
- Prompt: a reusable template the server offers the client, invoked from the
  client UI.
- Local server: a subprocess on the user's machine that speaks MCP over stdio.
- Remote server: a hosted server that speaks MCP over HTTP with Server-Sent
  Events.

## Architecture and Implementation

The client opens with `initialize`, declaring its protocol version and asking
what the server supports. It then calls `tools/list`, `resources/list`, and
`prompts/list`. Each entry carries a JSON Schema, so the model learns the call
shape. Invocation sends `tools/call` with a name and an arguments object. The
build runs in four steps. Step one installs an SDK: `pip install mcp` for
Python, or `npm install @modelcontextprotocol/sdk` for TypeScript. Step two
writes a 20-line server. Step three registers the server in the Claude Code
config under `mcpServers`, naming a command and an absolute path to the script.
The client launches the script as a subprocess and speaks stdio. Step four adds
a resource and a prompt through further decorators. The post treats tools as
the starting point and both others as later additions.

## Code Examples

The post carries four reusable fragments. A raw `tools/call` request and
response pair for a `create_issue` tool, showing the `jsonrpc`, `id`, `method`,
and `params` fields and a `content` array in the result. A complete Python
weather server built on `FastMCP("weather-server")`, where `@mcp.tool()`
derives the JSON Schema from type hints and the docstring, and `mcp.run()`
starts the JSON-RPC loop. A Claude Code config snippet mapping the server name
to a `command` and `args` pair. A `@mcp.resource("weather://history/{city}")`
declaration and a `@mcp.prompt()` declaration showing the URI template and the
prompt-return pattern.

## Best Practices

- Name a tool as a verb the agent would say. Write `search_issues`, not
  `issuesSearchV2`.
- Keep the tool surface small. Eight focused tools beat forty overlapping ones.
- Return a short structured result plus an identifier for detail on request.
- Write an error message that states the expected format and the value
  received.
- Require an explicit `confirm=true` parameter on any action that sends,
  spends, or deletes.
- Default to a local stdio server. Move to remote for a stated reason.
- Search the existing server catalogue before writing a new server.

## Warnings and Anti-Patterns

- A 50KB JSON blob in a tool result burns the agent's most expensive resource.
- A bare status code such as "400" gives the model no basis for its next step.
- A remote server adds deployment, auth, and observability work that a local
  subprocess avoids. Three cases justify that cost: shared team tooling,
  secrets that stay off laptops, and third-party access.
- Building a server from scratch past the first learning exercise repeats work
  a scaffold does faster.

## Related Concepts

- [[mcp]]
- [[tool-use]]
- [[claude-code]]
- [[best-practices-index]]
- [[10_Sources/Blog/mcp-101-build-your-first-server|MCP 101]]
- [[10_Sources/Blog/mcp-internals-client-server|MCP Internals]]
- [[10_Sources/Docs/mcp-introduction|What is MCP?]]
- [[10_Sources/Docs/mcp-builder-skill|MCP Builder Skill]]
- [[10_Sources/Books/mcp-illustrated-guidebook-chawla-pachaar-2025|MCP Illustrated Guidebook]]

## Future Work

The post forecasts that "does it have an MCP server?" replaces "does it have an
API?" as the first question teams ask of a new tool. It points to two of its
own playbooks: MCP Hub, a catalogue of servers for filesystem, Git, Postgres,
browser automation, and Slack, and MCP Server Builder, which generates a server
from a plain-English description of the tools wanted.

## References

- Claude Code Playbooks Blog, "The Complete Guide to MCP Servers: What They Are
  and How to Build One", 16 April 2026. URL TBD.
- Related playbooks named in the post: MCP Hub, MCP Server Builder.
