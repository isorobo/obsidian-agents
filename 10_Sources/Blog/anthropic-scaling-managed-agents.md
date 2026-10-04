---
type: source
status: draft
created: 2026-10-04
title: "Scaling Managed Agents: Decoupling the brain from the hands"
authors:
- Lance Martin
- Gabe Cemaj
- Michael Cohen
organisation: Anthropic
source_type: blog
venue: Anthropic Engineering
url: https://www.anthropic.com/engineering/managed-agents
year: 2026
date_published: 2026-04-08
anthropic: true
topic:
- topic/architectures
- topic/deployment
- topic/security
tags:
- managed-agents
- harness
- sandbox
- session-log
- credentials
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-engineering
af_targets:
- af:ADR-0006
- af:ADR-0004
- af:RSCH-04/Q21
- af:RSCH-04/Q23
- af:RSCH-04/Q22
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 2aa36bb936abdc770a5bea20f3050db5bb7164f654b63f725e4f14333adf8cf8
---

# Scaling Managed Agents: Decoupling the brain from the hands

> Lance Martin, Gabe Cemaj and Michael Cohen, "Scaling Managed Agents: Decoupling the brain from the hands", Anthropic Engineering, 8 April 2026, https://www.anthropic.com/engineering/managed-agents.

## Summary

The post describes Managed Agents, a hosted agent service built on three decoupled parts: the brain (Claude plus its harness), the hands (sandboxes, tools and MCP servers) and the session (a durable event log). Each part sits behind a stable interface so any can fail or be replaced without disturbing the others. The design follows the operating system habit of virtualising resources so abstractions outlast implementations. Provisioning containers only when needed cut time-to-first-token by about 60% at p50 and over 90% at p95.

## Key Concepts

- Brain, hands and session as separate components with standard interfaces.
- Cattle not pets: stateless, replaceable harnesses and sandboxes.
- The session log is context held outside the model's context window and read back via `getEvents()`.
- Credentials live in vaults and are unreachable from sandboxes running Claude-generated code.

## Terminology

- Brain: Claude and its harness.
- Hands: execution environments such as containers, tools and MCP servers.
- Harness: the loop that calls Claude and routes tool calls.

## Architecture and Implementation

The harness is stateless and recovers by replaying the session event log. Sandboxes are provisioned on demand. Authentication is bundled with a resource at initialisation, and an MCP proxy pattern keeps OAuth tokens in a secure vault away from generated code.

## Code Examples

The source carries no reusable code beyond the `getEvents()` interface name.

## Best Practices

- Separate recoverable storage (the session) from context management (the harness).
- Bundle auth with resources at initialisation rather than passing credentials around.
- Use an MCP proxy with tokens held in a vault.
- Treat harness assumptions as perishable; the post notes they go stale as models improve.

## Warnings and Anti-Patterns

- Long-lived pet containers that hold state.
- Placing credentials where model-generated code can reach them.

## Related Concepts

- [[the-agent-loop]]
- [[claude-agent-sdk]]
- [[mcp]]
- [[memory]]

## Future Work

The post frames the interfaces as meant to outlast any one harness implementation as models change.

## References

- https://www.anthropic.com/engineering/managed-agents
