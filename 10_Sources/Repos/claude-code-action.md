---
type: source
status: draft
created: 2026-10-04
title: "Claude Code Action"
authors:
- Anthropic
organisation: Anthropic
source_type: repo
venue: GitHub
url: https://github.com/anthropics/claude-code-action
year: 2025
date_published: 2025-05-19
anthropic: true
topic:
- topic/claude-code
- topic/deployment
tags:
- github-actions
- code-review
- automation
- ci
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-github
af_targets:
- af:RSCH-01/claude-code
- cf:adapter/claude-code
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: cb8975e9940de0c9d0f5abfaedc05095d4150dcea1d670b94df4e0975c40cdda
---

# Claude Code Action

> Anthropic, "Claude Code Action", GitHub (anthropics), repository created 19 May 2025, https://github.com/anthropics/claude-code-action.

## Summary

A GitHub Action that runs Claude Code inside a workflow to review pull requests, implement changes and answer technical questions on issues and PRs. It detects when to activate from the workflow context. Triggers include `@claude` mentions in comments, issue assignment, explicit prompts in automation workflows and custom conditions. Setup is either the `/install-github-app` command in Claude Code (Anthropic API users) or a manual configuration for AWS Bedrock, Google Vertex AI or Microsoft Foundry. The README is short and defers detail to linked documentation. Licence is MIT.

## Key Concepts

- Core inputs are `prompt` (the instruction) and `claude_args` (extra CLI configuration), plus provider credentials.
- The action runs on the user's own GitHub runner; model calls go to the chosen provider.
- Typical uses: PR review, security analysis, issue triage and labelling, documentation sync, path-specific triggers.
- Commit signing is supported.

## Terminology

- claude_args: arguments passed through to Claude Code.
- @claude mention: the comment trigger.

## Architecture and Implementation

The action needs GitHub API access to read PRs and issues and write comments, with configurable file operation permissions. Repository admin access is needed to install the app and set secrets.

## Code Examples

The source README carries no reusable code.

## Best Practices

- Scope permissions to what the workflow needs.
- Use path-specific triggers to limit when the agent runs.
- Read the access control and limitations documents before enabling on public repositories.

## Warnings and Anti-Patterns

- The README points to a "Capabilities and Limitations" document for what Claude cannot do; it was not fetched here.
- Granting broad repository permissions to an agent triggered by comments widens the attack surface.

## Related Concepts

- [[claude-code]]
- [[claude-agent-sdk]]
- [[workflow-vs-autonomous-agent]]

## Future Work

None stated.

## References

- https://github.com/anthropics/claude-code-action
