---
type: source
status: draft
created: 2026-10-04
title: "Claude Agent SDK for Python"
authors:
- Anthropic
organisation: Anthropic
source_type: repo
venue: GitHub
url: https://github.com/anthropics/claude-agent-sdk-python
year: 2025
date_published: 2025-06-11
anthropic: true
topic:
- topic/claude-sdk
- topic/tool-use
tags:
- claude-agent-sdk
- python
- hooks
- in-process-mcp
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-github
af_targets:
- af:RSCH-01/claude-code
- af:DELEG-02
- af:ADR-0004
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: abfcb5d148a9d201eb11e56b30633626d8ef7246775e9c7618d14170729a3936
---

# Claude Agent SDK for Python

> Anthropic, "Claude Agent SDK for Python", GitHub (anthropics), repository created 11 June 2025, https://github.com/anthropics/claude-agent-sdk-python.

## Summary

The repository holds the Python SDK that lets a program drive Claude Code programmatically. The README describes two entry points: `query()`, an async function that returns an iterator of messages for one-shot use, and `ClaudeSDKClient` for bidirectional conversations with custom tools and hooks. The package installs with `pip install claude-agent-sdk`, needs Python 3.10 or later, and bundles the Claude Code CLI, so no separate install is required. Recent releases (v0.2.153 to v0.2.163, September 2026) mostly bump the bundled CLI version, with behaviour changes such as a `snapshot` option for system prompts, a `verbatim_prompts` option and a fix for background subagent follow-ups. The release page was read for this note; the README is the main grounding.

## Key Concepts

- `query()` is the simplest path: a prompt in, an async stream of messages out.
- `ClaudeSDKClient` keeps a session open for multi-turn exchange, custom tools and hooks.
- `ClaudeAgentOptions` carries configuration: `system_prompt`, `cwd`, `max_turns`, `cli_path`, `mcp_servers`, `allowed_tools`, `disallowed_tools`, `permission_mode`, `hooks`.
- SDK MCP servers run in-process, so custom tools are plain Python functions with no subprocess to manage.
- Hooks are Python functions called at points in the agent loop (for example `PreToolUse`) to give deterministic control the model does not see.
- `allowed_tools` is an auto-approve allowlist, not a restriction on the toolset.

## Terminology

- SDK MCP server: an MCP server created with `create_sdk_mcp_server` that runs inside the host process.
- HookMatcher: pairs a tool-name matcher with hook callbacks.
- permission_mode: sets automatic acceptance behaviour, for example `acceptEdits`.

## Architecture and Implementation

The SDK wraps the bundled Claude Code CLI as a subprocess and exposes its message stream as typed Python objects (`AssistantMessage`, `UserMessage`, `SystemMessage`, `ResultMessage`, with `TextBlock`, `ToolUseBlock`, `ToolResultBlock` content). Custom tools register through the `@tool` decorator and an in-process MCP server. External MCP servers can be mixed in as stdio configurations. Errors surface as a typed hierarchy: `ClaudeSDKError`, `CLINotFoundError`, `CLIConnectionError`, `ProcessError`, `ResultError`, `CLIJSONDecodeError`.

## Code Examples

```python
from claude_agent_sdk import ClaudeSDKClient, ClaudeAgentOptions

options = ClaudeAgentOptions(
    system_prompt="You are a helpful assistant"
)

async with ClaudeSDKClient(options=options) as client:
    await client.query("Tell me a joke")
    async for msg in client.receive_response():
        print(msg)
```

The README also shows a `PreToolUse` hook that denies a Bash command containing a given pattern, and an in-process `greet` tool.

## Best Practices

- Use `disallowed_tools` to block a tool, because `allowed_tools` only auto-approves.
- Prefer in-process SDK MCP servers for tools you own: simpler debugging and no subprocess overhead.
- Use hooks for rules that must hold regardless of model behaviour.
- Catch the typed exceptions and inspect `ResultError` for the terminal reason.

## Warnings and Anti-Patterns

- Assuming an unlisted tool is unavailable: it falls through to `permission_mode` and `can_use_tool`.
- Use is governed by Anthropic's Commercial Terms of Service, with component licences in each LICENSE file.
- System prompts are cached by default, so set the snapshot option to false when iterating on them.

## Related Concepts

- [[claude-agent-sdk]]
- [[claude-code]]
- [[tool-use]]
- [[mcp]]
- [[the-agent-loop]]

## Future Work

The README states none. The release stream shows ongoing CLI alignment and option additions.

## References

- https://github.com/anthropics/claude-agent-sdk-python
- https://github.com/anthropics/claude-agent-sdk-python/releases
