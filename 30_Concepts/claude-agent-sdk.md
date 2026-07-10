---
type: concept
status: draft
created: 2026-07-10
name: Claude Agent SDK
slug: claude-agent-sdk
topic:
- topic/claude-sdk
tags: [agent-sdk, python, typescript, agent-loop, context-management, subagents]
synonyms: [Claude Agent SDK, Agent SDK]
defined_in: "[[10_Sources/Docs/claude-agent-sdk-overview|Agent SDK overview]]"
related_concepts: ["[[the-agent-loop]]", "[[tool-use]]", "[[claude-code]]"]
anthropic: true
---

# Claude Agent SDK

> The Claude Agent SDK is a Python and TypeScript library that runs the Claude Code agent loop inside your own process.

## Summary

The Claude Agent SDK builds production agents from the components that power Claude Code. It gives the same tools, agent loop, and context management as a library. Claude owns the loop. The developer describes the task and the allowed tools. The SDK runs the model, executes tools, compacts context, and streams messages until a final result.

## Key Concepts

- The SDK runs in the developer process, not a hosted sandbox.
- Built-in tools include Read, Write, Edit, Bash, Glob, Grep, WebSearch, and WebFetch.
- Hooks, subagents, MCP servers, permissions, and sessions extend the agent.

## Detail

The `query` function takes a prompt and `ClaudeAgentOptions`. Options set `allowed_tools`, hooks, subagent definitions, MCP servers, and a permission mode. The Client SDK differs: there the developer writes the tool loop by checking `stop_reason` and feeding results back. The Agent SDK handles that cycle. It also loads `.claude/` configuration, skills, commands, and `CLAUDE.md`. Managed Agents offer a hosted REST alternative that runs on Anthropic infrastructure. A common path prototypes with the SDK, then moves to Managed Agents for scale.

## Trade-offs and Limits

The SDK cuts the boilerplate of a hand-written tool loop. It suits CI pipelines, custom applications, and production automation. The developer runs and secures the process and its filesystem. claude.ai login for third-party products is not permitted, so use API key authentication. Context compaction helps long runs, yet a long session still costs tokens.

## Related

- [[the-agent-loop]]
- [[tool-use]]
- [[claude-code]]

## Sources

- [[10_Sources/Docs/claude-agent-sdk-overview|Agent SDK overview]]
- https://code.claude.com/docs/en/agent-sdk/overview

## See also

- [[MOC - Claude SDK]]
