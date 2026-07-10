---
type: concept
status: draft
created: 2026-07-10
name: Claude Code
slug: claude-code
topic:
- topic/claude-code
tags: [claude-code, cli, ide, agentic-coding, mcp, hooks]
synonyms: [Claude Code]
defined_in: "[[10_Sources/Docs/claude-code-overview|Claude Code overview]]"
related_concepts: ["[[claude-agent-sdk]]", "[[mcp]]", "[[the-agent-loop]]"]
anthropic: true
---

# Claude Code

> Claude Code is Anthropic's agentic coding tool that reads a codebase, edits files, runs commands, and integrates with developer tools.

## Summary

Claude Code turns a plain-language request into working code. It plans an approach, edits across many files, and verifies the result. It runs in the terminal, IDE, desktop app, and browser. Each surface connects to the same engine. A `CLAUDE.md` file, settings, and MCP servers carry across every surface.

## Key Concepts

- The Terminal CLI drives edits and commands from the command line.
- CLAUDE.md sets standards and context Claude Code reads each session.
- MCP connects Claude Code to Google Drive, Jira, Slack, and custom tools.

## Detail

A native installer sets up the CLI on macOS, Linux, WSL, and Windows. VS Code and JetBrains extensions add inline diffs and plan review. Claude Code works with git to stage changes, write commit messages, and open pull requests. Skills package repeatable workflows a team shares. Hooks run shell commands before or after an action, such as formatting after an edit. Subagents split one task across agents that a lead coordinates. The Agent SDK exposes the same tools for custom agents. Routines run scheduled work on Anthropic-managed infrastructure.

## Trade-offs and Limits

Claude Code shortens tedious work: tests, lint fixes, dependency updates, and release notes. It reads a whole codebase and acts across files. Broad autonomy needs guardrails, so permissions and hooks bound the risk. An agent that edits and runs commands can break a build, which makes review and version control essential.

## Related

- [[claude-agent-sdk]]
- [[mcp]]
- [[the-agent-loop]]

## Sources

- [[10_Sources/Docs/claude-code-overview|Claude Code overview]]
- https://code.claude.com/docs/en/overview

## See also

- [[MOC - Claude Code]]
