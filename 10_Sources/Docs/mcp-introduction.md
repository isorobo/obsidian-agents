---
type: source
status: draft
created: 2026-07-10
title: What is the Model Context Protocol (MCP)?
authors: []
organisation: Anthropic
source_type: docs
venue: modelcontextprotocol.io
url: https://modelcontextprotocol.io/docs/getting-started/intro
year: 2024
date_published: 2024-11-25
anthropic: true
topic:
- topic/mcp
- topic/tool-use
tags: [mcp, protocol, tools, resources, prompts]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# What is the Model Context Protocol (MCP)?

> Anthropic, "What is the Model Context Protocol (MCP)?", modelcontextprotocol.io, 2024. https://modelcontextprotocol.io/docs/getting-started/intro

## Summary

The Model Context Protocol is an open standard for connecting AI applications to external systems. Anthropic introduced it on 25 November 2024. The protocol replaces fragmented custom integrations with one interface. The docs compare MCP to a USB-C port for AI applications. A client application connects to servers that expose data sources, tools, and workflows.

## Key Concepts

- MCP standardises how an AI application reaches external data and actions.
- The protocol is open and supported across many clients and servers.
- Claude, ChatGPT, VS Code, and Cursor act as MCP clients.

## Terminology

- MCP client — the AI application that connects to servers.
- MCP server — the process that exposes tools, resources, and prompts.
- Tool — an executable function the model calls.
- Resource — file-like structured data the model reads.
- Prompt — a predefined template that guides interaction.

## Architecture and Implementation

A developer exposes data through an MCP server or builds a client that connects to servers. The specification and SDKs live on GitHub. Anthropic shipped pre-built servers for Google Drive, Slack, GitHub, Git, Postgres, and Puppeteer.

## Code Examples

The docs point to build-server and build-client guides for reference implementations.

## Best Practices

- Build once against MCP and integrate across many clients.
- Reuse published servers before writing a new one.

## Warnings and Anti-Patterns

- Custom point-to-point integrations create silos that MCP removes.

## Related Concepts

- [[mcp]]
- [[tool-use]]

## Future Work

The protocol continues to grow across clients, servers, and app extensions.

## References

- https://modelcontextprotocol.io/docs/getting-started/intro
- https://www.anthropic.com/news/model-context-protocol
