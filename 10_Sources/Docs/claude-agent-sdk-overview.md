---
type: source
status: draft
created: 2026-07-10
title: Claude Agent SDK overview
authors: []
organisation: Anthropic
source_type: docs
venue: code.claude.com
url: https://code.claude.com/docs/en/agent-sdk/overview
year: 2026
date_published: 
anthropic: true
topic:
- topic/claude-sdk
- topic/tool-use
tags: [agent-sdk, python, typescript, agent-loop, tools]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Claude Agent SDK overview

> Anthropic, "Agent SDK overview", code.claude.com, 2026. https://code.claude.com/docs/en/agent-sdk/overview

## Summary

The Claude Agent SDK builds production agents with Claude Code as a library. It gives the same tools, agent loop, and context management that power Claude Code. The SDK ships in Python and TypeScript. Claude owns the loop: the SDK runs the model, executes tools, manages context, and streams messages until a final result.

## Key Concepts

- The SDK runs the agent loop inside the developer process.
- Built-in tools cover file operations, search, shell, and web access.
- Hooks, subagents, MCP, permissions, and sessions extend the agent.

## Terminology

- Agent loop — the model-tool-result cycle the SDK runs.
- Client SDK — the direct API library where the developer writes the tool loop.
- Managed Agents — the hosted REST alternative that runs on Anthropic infrastructure.

## Architecture and Implementation

The `query` function accepts a prompt and `ClaudeAgentOptions`. Options set `allowed_tools`, hooks, subagent definitions, MCP servers, permission mode, and session resume. The SDK loads `.claude/` configuration, skills, commands, and `CLAUDE.md`. Context compaction triggers as the conversation approaches its limit.

## Code Examples

```python
from claude_agent_sdk import query, ClaudeAgentOptions
```

The docs show a bug-fixing agent with `allowed_tools=["Read", "Edit", "Bash"]`.

## Best Practices

- Restrict `setting_sources` to control which configuration loads.
- Prototype with the SDK, then move to Managed Agents for production scale.

## Warnings and Anti-Patterns

- claude.ai login for third-party products is not permitted. Use API key authentication.

## Related Concepts

- [[claude-agent-sdk]]
- [[the-agent-loop]]
- [[tool-use]]

## Future Work

The changelog tracks new tools and features for both language SDKs.

## References

- https://code.claude.com/docs/en/agent-sdk/overview
- https://github.com/anthropics/claude-agent-sdk-python
