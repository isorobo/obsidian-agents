---
type: source
status: draft
created: 2026-10-04
title: "Claude Agent SDK for TypeScript"
authors:
- Anthropic
organisation: Anthropic
source_type: repo
venue: GitHub
url: https://github.com/anthropics/claude-agent-sdk-typescript
year: 2025
date_published: 2025-09-27
anthropic: true
topic:
- topic/claude-sdk
- topic/release-notes
tags:
- claude-agent-sdk
- typescript
- npm
- releases
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-github
af_targets:
- af:RSCH-01/claude-code
- cf:adapter/claude-code
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 12a8347ec501b2c5f39eb28a0aca793064da2af4b654f7961f35af88dee38288
---

# Claude Agent SDK for TypeScript

> Anthropic, "Claude Agent SDK for TypeScript", GitHub (anthropics), repository created 27 September 2025, https://github.com/anthropics/claude-agent-sdk-typescript.

## Summary

This repository distributes the TypeScript package `@anthropic-ai/claude-agent-sdk`, which lets developers build agents with Claude Code's capabilities: understanding codebases, editing files, running commands and executing multi-step workflows. The README is thin. It gives the install command (`npm install @anthropic-ai/claude-agent-sdk`, Node.js 18 or later), links to the official documentation and a migration guide, and states that the Claude Code SDK has been superseded by the Agent SDK. The release stream (v0.3.280 to v0.3.289, 22 September to 3 October 2026) is where the behaviour detail lives, with a release almost daily that tracks the Claude Code CLI version.

## Key Concepts

- The package is the TypeScript counterpart of the Python SDK and shares the Claude Code runtime.
- Versions track Claude Code closely: v0.3.288 and v0.3.289 align with Claude Code 2.1.288 and 2.1.289.
- Release notes record SDK-visible changes such as MCP server lifecycle fixes, SDK MCP manifest tracking, session forking fixes, and permission prompt cancellation fixes.
- A lightweight `/core` entry point for bundled applications and process prewarming appeared in v0.3.282.
- The package size fell from 1.47 MB to 0.97 MB in v0.3.281.

## Terminology

- Session forking: branching a stored conversation into a new session.
- Prewarming: starting the underlying process before the first prompt to cut latency.
- Managed settings: organisation-level configuration, which gained marketplace allowlists and blocklists.

## Architecture and Implementation

The README documents no API surface and defers to the official documentation at docs.claude.com. Architecture is therefore inferred only from release notes: the SDK wraps the Claude Code runtime, forwards its init messages (plugin errors, startup failure reasons) and exposes MCP and permission callbacks.

## Code Examples

The source carries no reusable code beyond the install command: `npm install @anthropic-ai/claude-agent-sdk`.

## Best Practices

- Read the official documentation rather than the README for API detail.
- Pin the SDK version and read release notes on upgrade, since permission mode defaults and background-operation handling changed within a few days in late September 2026.

## Warnings and Anti-Patterns

- The README states the SDK collects feedback data (usage, conversation data) with limited retention and says it is not used for model training.
- Migrating from the old Claude Code SDK needs the migration guide.

## Related Concepts

- [[claude-agent-sdk]]
- [[claude-code]]
- [[mcp]]

## Future Work

No roadmap is stated. Fast release cadence suggests continuing alignment with Claude Code.

## References

- https://github.com/anthropics/claude-agent-sdk-typescript
- https://github.com/anthropics/claude-agent-sdk-typescript/releases
- https://docs.claude.com/en/api/agent-sdk/overview
