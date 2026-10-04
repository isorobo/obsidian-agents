---
type: source
status: draft
created: 2026-07-11
title: "MCP Internals: STDIO, SSE, and JSON-RPC Explained"
authors:
- Shirley
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 3.2
url: https://www.aibuilderclub.com/blog/mcp-internals-client-server
year: 2026
date_published: 2026-06-11
anthropic: false
topic:
- topic/mcp
tags:
- mcp
- json-rpc
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
af_targets:
- af:DELEG-02
- af:RSCH-04/Q23
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 6f131aa9fbee6a32ac26e95c99683d444fbc4c44443019359d8fe91c76dfe668
---

# MCP Internals: STDIO, SSE, and JSON-RPC Explained

> Shirley, "MCP Internals: STDIO, SSE, and JSON-RPC Explained", AI Builder Club, Build AI Agents Course, 11 June 2026, https://www.aibuilderclub.com/blog/mcp-internals-client-server.

## Summary

Where 3.1 builds a server, this lesson opens it up: an MCP config file is a shell command disassembled into JSON, and the client reassembles and spawns it as an ordinary local process — no different in kind from anything else launched from a shell. Everything else follows from that: stdio transport for local servers relies on process isolation, not authentication, for its security model; SSE carries the same JSON-RPC messages over HTTP for remote servers; and the entire agent loop, at the protocol level, is six repeating steps and nothing more.

## Key Concepts

- Two transports serve two deployment shapes: stdio (stdin/stdout piping, no network layer, instant, secured by process isolation) for local servers, and SSE (HTTP-based) for remote ones, which trades instant response for the need for real authentication.
- JSON-RPC 2.0 pairs every request and response by `id`, carrying `method` and `params` on the way out and a result or a structured `error` field on the way back; `tools/list` and `tools/call` are the two methods that matter most in practice.
- The full agentic loop reduces to six steps: the client collects tool catalogues, sends the question plus tools to the model, the model returns tool-call intent as JSON, the client executes the actual call, the result loops back to the model, and the model synthesises a final answer once satisfied.
- Two schools give the model tool awareness: native function calling via the API's `tools` parameter (clean, constrained-decoded, requires tool-use fine-tuning) versus embedding the whole tool protocol as text in the system prompt (works with any model, burns tokens, risks format drift).

## Terminology

- STDIO — standard input/output piping used for local, same-machine client-server communication with no network layer.
- SSE (Server-Sent Events) — an HTTP-based transport carrying JSON-RPC messages for a remote MCP server.
- JSON-RPC 2.0 — the request/response message format MCP uses over either transport, pairing calls and results by a shared `id`.

## Architecture and Implementation

The lesson traces a full six-step loop through a worked teacher-course database query, then gives pseudocode for a minimal toy client: spawn the configured servers, collect their tool catalogues via `tools/list`, loop with the model by sending messages plus the catalogue, route any resulting tool call to its owning server via `tools/call`, and append the result back into the message history. It recommends logging all JSON traffic during development, both to understand client behaviour and as a security audit trail.

## Code Examples

A raw JSON-RPC message piped directly to a filesystem server over stdin, a matched `tools/call` request/response pair, and pseudocode for a complete minimal MCP client loop.

## Best Practices

- Log all JSON-RPC traffic during development; it doubles as documentation and a security audit trail.
- Prefer local command-line servers over remote `npx`-fetched ones where offline immunity and predictability matter.
- On Windows, wrap Unix-style commands in `cmd /c` rather than assuming a bare command will resolve.

## Warnings and Anti-Patterns

- Assuming authentication secures a local stdio server is a category error; the actual security boundary is process isolation, and a malicious local server runs with the launching process's permissions regardless.
- System-prompt-based tool awareness is more format-fragile and token-expensive than native function calling; treating the two as interchangeable ignores a real reliability and cost difference.

## Related Concepts

- [[mcp]]
- [[the-agent-loop]]
- [[tool-use]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson defers the security implications of "an MCP server is just a spawned local process" to 3.3, which enumerates concrete attack vectors on exactly this trust model.

## References

- MCP Internals: STDIO, SSE, and JSON-RPC Explained — https://www.aibuilderclub.com/blog/mcp-internals-client-server
