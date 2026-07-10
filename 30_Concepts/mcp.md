---
type: concept
status: draft
created: 2026-07-10
name: Model Context Protocol (MCP)
slug: mcp
topic:
- topic/mcp
- topic/tool-use
tags: [mcp, protocol, tools, resources, prompts, integration]
synonyms: [MCP, Model Context Protocol]
defined_in: "[[10_Sources/Docs/mcp-introduction|What is MCP?]]"
related_concepts: ["[[tool-use]]", "[[claude-agent-sdk]]", "[[claude-code]]"]
anthropic: true
---

# Model Context Protocol (MCP)

> MCP is an open standard that connects an AI application to external tools, data, and prompts through one interface.

## Summary

The Model Context Protocol standardises how an agent reaches the outside world. Anthropic introduced it on 25 November 2024. Before MCP, each data source needed a custom integration. MCP replaces those point-to-point links with one protocol. An agent gains reliable access to files, databases, and services. The docs compare MCP to a USB-C port for AI applications.

## Key Concepts

- MCP defines a client and a server role.
- A server exposes three primitives: tools, resources, and prompts.
- One integration works across many clients and servers.

## Detail

An MCP client lives inside the AI application. Claude, Claude Code, and other assistants act as clients. An MCP server exposes capabilities to that client. A tool is an executable function the model calls. A resource is file-like data the model reads. A prompt is a template that shapes the interaction. The client discovers what a server offers, then the model uses it during the agent loop. Anthropic published servers for Google Drive, Slack, GitHub, Git, Postgres, and Puppeteer.

## Trade-offs and Limits

MCP removes integration sprawl and gives one surface for tools. The gain grows with the number of sources an agent touches. The protocol adds a server process to run and secure. Each server widens the attack surface, so access control and input validation matter. A single tool call still costs latency and tokens.

## Related

- [[tool-use]]
- [[claude-agent-sdk]]
- [[claude-code]]

## Sources

- [[10_Sources/Docs/mcp-introduction|What is MCP?]]
- https://www.anthropic.com/news/model-context-protocol

## See also

- [[MOC - MCP]]
