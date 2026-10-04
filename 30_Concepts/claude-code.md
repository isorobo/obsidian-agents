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
af_targets:
- af:RSCH-01/claude-code
wiki_indexed: '2026-10-04T03:42:35Z'
wiki_hash: 6d9728b3c6b75f79186639426e02618850e66f18ead4e4e800db04a0ec4728df
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
- [[10_Sources/Blog/anthropic-how-we-contain-claude|How we contain Claude across products]]
- [[10_Sources/Blog/agent-modes-plan-default-auto|Plan vs Default vs Auto Mode]]
- [[10_Sources/Blog/agent-sandbox-os-level-security|Agent Sandboxes: OS-Level Security]]
- [[10_Sources/Blog/anthropic-april-23-postmortem|An update on recent Claude Code quality reports]]
- [[10_Sources/Blog/anthropic-claude-code-auto-mode|How we built Claude Code auto mode]]
- [[10_Sources/Docs/claude-code-headless-mode|Run Claude Code programmatically]]
- [[10_Sources/Docs/claude-code-hooks-reference|Claude Code hooks reference]]
- [[10_Sources/Docs/claude-code-permissions|Claude Code permissions]]
- [[10_Sources/Release-Notes/claude-code-2-1-285-2026-09-29|Claude Code 2.1.285]]
- [[10_Sources/Release-Notes/claude-code-2-1-286-2026-09-30|Claude Code 2.1.286]]
- [[10_Sources/Release-Notes/claude-code-2-1-287-2026-10-01|Claude Code 2.1.287]]
- [[10_Sources/Release-Notes/claude-code-2-1-288-2026-10-02|Claude Code 2.1.288]]
- [[10_Sources/Release-Notes/claude-code-2-1-289-2026-10-03|Claude Code 2.1.289]]
- [[10_Sources/Release-Notes/claude-opus-5-5-2026-09-22|Claude Opus 5.5]]
- [[10_Sources/Release-Notes/claude-sonnet-5-5-2026-09-28|Claude Sonnet 5.5]]
- [[10_Sources/Repos/anthropic-skills-repository|Anthropic Agent Skills Repository]]
- [[10_Sources/Repos/claude-agent-sdk-python|Claude Agent SDK for Python]]
- [[10_Sources/Repos/claude-agent-sdk-typescript|Claude Agent SDK for TypeScript]]
- [[10_Sources/Repos/claude-code-action|Claude Code Action]]
- [[10_Sources/Repos/learn-agent-architecture|learn-agent-architecture]]
- [[10_Sources/Repos/sandbox-runtime|Anthropic Sandbox Runtime]]
- [[10_Sources/Talks/boris-cherny-building-claude-code-yc-2026|Boris Cherny: Building Claude Code]]
- [[10_Sources/Talks/boris-cherny-peterman-pod-career-claude-code|Boris Cherny on How His Career Grew]]

## See also

- [[MOC - Claude Code]]
