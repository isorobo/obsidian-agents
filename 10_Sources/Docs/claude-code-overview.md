---
type: source
status: draft
created: 2026-07-10
title: Claude Code overview
authors: []
organisation: Anthropic
source_type: docs
venue: code.claude.com
url: https://code.claude.com/docs/en/overview
year: 2026
date_published: 
anthropic: true
topic:
- topic/claude-code
tags: [claude-code, cli, ide, mcp, hooks, subagents]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Claude Code overview

> Anthropic, "Overview", code.claude.com, 2026. https://code.claude.com/docs/en/overview

## Summary

Claude Code is an agentic coding tool. It reads a codebase, edits files, runs commands, and integrates with developer tools. It runs in the terminal, IDE, desktop app, and browser. Each surface connects to the same engine, so `CLAUDE.md` files, settings, and MCP servers work across all of them.

## Key Concepts

- The Terminal CLI edits files and runs commands from the command line.
- The VS Code and JetBrains extensions add inline diffs and plan review.
- Routines run scheduled tasks on Anthropic-managed infrastructure.

## Terminology

- CLAUDE.md — a markdown file Claude Code reads at the start of every session.
- Auto memory — learnings Claude saves across sessions without manual writing.
- Skills — packaged workflows a team shares, invoked as `/name`.
- Hooks — shell commands run before or after Claude Code actions.
- Subagents — multiple agents that split one task, coordinated by a lead.

## Architecture and Implementation

A native installer sets up the CLI on macOS, Linux, WSL, and Windows. Claude Code works with git to stage changes, write commit messages, and open pull requests. MCP connects Claude Code to Google Drive, Jira, Slack, and custom tooling. The Agent SDK exposes the same tools for custom agents.

## Code Examples

```bash
claude "write tests for the auth module, run them, and fix any failures"
```

## Best Practices

- Set coding standards and review checklists in `CLAUDE.md`.
- Package repeatable workflows as skills for the team.

## Warnings and Anti-Patterns

- Hidden project rules cause drift. Record them in `CLAUDE.md` instead.

## Related Concepts

- [[claude-code]]
- [[mcp]]
- [[claude-agent-sdk]]

## Future Work

The docs track new surfaces such as Remote Control, Channels, and web sessions.

## References

- https://code.claude.com/docs/en/overview
- https://code.claude.com/docs/en/memory
