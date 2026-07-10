---
type: source
status: draft
created: 2026-07-10
title: "MCP: The Illustrated Guidebook"
authors:
- Avi Chawla
- Akshay Pachaar
organisation: "Daily Dose of Data Science"
source_type: book
venue: "Daily Dose of Data Science, Free 2025 Edition"
url: TBD
year: 2025
date_published: 2025
anthropic: false
topic:
- topic/mcp
tags: [mcp, illustrated-guide, tool-use, client-server, protocol-design]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# MCP: The Illustrated Guidebook

> Full citation: Chawla, A. and Pachaar, A. "MCP: The Illustrated Guidebook." Daily Dose of Data Science, 2025.

## Summary

This 74-page illustrated guide from Daily Dose of Data Science explains the Model Context Protocol (MCP) in two sections. Section one covers the protocol itself: what MCP is, why it was created, its host-client-server architecture, and its three core capabilities, tools, resources, and prompts. Section two walks through eleven worked MCP projects, including a local MCP client, an agentic RAG system, a financial analyst, a voice agent, a unified MCP server, shared memory across Claude Desktop and Cursor, and a deep researcher. The authors pitch the book at a range of readers and offer a short self-assessment to route readers to the chapters most relevant to their expertise. The fetched pages cover the protocol section in full; the project chapters sit beyond the fetched range.

## Key Concepts

- MCP standardises how AI models connect to external tools, resources, and environments, replacing one-off integrations.
- The M×N integration problem: M applications and N tools once needed M×N custom integrations.
- MCP reduces this to M+N implementations: each application builds one client, each tool builds one server.
- Three roles compose the architecture: host, client, and server.
- Three capability types compose the protocol surface: tools, resources, and prompts.

## Terminology

- **Host** — the user-facing AI application, such as Claude Desktop or an AI-enhanced IDE, that initiates server connections and manages conversation state.
- **Client** — the component inside the host that handles low-level MCP communication with a server.
- **Server** — the external program that exposes tools, resources, and prompts in a standard format.
- **Tool** — an executable, model-controlled action, often with side effects, exposed through `tools/call`.
- **Resource** — a read-only, host-controlled data source retrieved through a URI, such as `file://path`.
- **Prompt** — a predefined template or multi-turn workflow that a server supplies, typically user- or developer-controlled.
- **M×N problem** — the combinatorial integration burden MCP was designed to remove.

## Architecture and Implementation

The guide presents MCP as a client-server architecture, similar in shape to the web, with terminology adapted to the AI context. The host is the user-facing application. It captures user input, keeps conversation history, and initiates connections to available MCP servers when the system needs them. The client sits inside the host and handles the low-level protocol communication. The authors describe the client as an adapter: the host decides what to do, and the client knows how to speak MCP to carry that decision out.

The server is the external program that exposes capabilities. It advertises what it can do in a standard format so a client can query and understand available tools, then executes requests from the client and returns results. Servers can run locally alongside the host or remotely on a cloud service.

The guide illustrates the pre-MCP world as M×N custom integrations, one per application-tool pair, and the post-MCP world as M+N implementations, since each application and each tool need only implement one side of the protocol once. The book compares MCP to a universal translator and, separately, to USB-C: a single standardised connector replacing a proliferation of incompatible interfaces.

On capabilities, the guide draws three control distinctions. Tools are model-controlled: the LLM decides when to call one, often behind a user permission prompt, since tools can trigger file I/O or network calls. Resources are host-controlled: the application decides when to fetch a resource and feeds it to the model as context, without giving the model open-ended access. Prompts are user- or developer-controlled: a client fetches a predefined template, often at the start of an interaction, to structure the conversation before the model responds.

## Code Examples

The guide shows a Python tool registered with the `@mcp.tool()` decorator, illustrating how a server function such as `get_weather(location)` becomes callable through `tools/call`. A parallel example shows a resource declared with `@mcp.resource("file://{path}")`, mapping a URI template to a `read_file` function. A third example shows a prompt function returning a list of message objects that pre-configure a code-review scenario before the model generates a reply.

## Best Practices

- Require explicit user permission before a tool call executes, since tools can have side effects.
- Keep resource access under host control rather than letting the model read arbitrarily.
- Identify resources by a stable URI or name rather than exposing them as free-form functions.
- Move reusable prompt templates to the server so they can be updated without changing the client application.

## Warnings and Anti-Patterns

- Hard-coding per-tool integration logic reproduces the M×N problem the protocol exists to remove.
- Granting a model unrestricted resource access risks reading data it should not see.
- Treating prompts as a way to smuggle instructions blurs the line between data and instruction, a risk the authors flag directly.

## Related Concepts

- [[mcp]]
- [[tool-use]]
- [[claude-agent-sdk]]

## Future Work

The fetched pages do not cover the eleven project chapters (local MCP client, agentic RAG, financial analyst, voice agent, unified MCP server, shared memory for Claude Desktop and Cursor, RAG over complex documents, synthetic data generator, deep researcher, RAG over videos, and audio analysis toolkit). A follow-up extraction of pages 20 to 74 would capture the applied, code-level detail behind each project.

## References

- Daily Dose of Data Science self-assessment link cited in the book: https://bit.ly/mcp-assessment
