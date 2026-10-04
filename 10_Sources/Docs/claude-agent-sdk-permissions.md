---
type: source
status: draft
created: 2026-10-04
title: "Configure permissions (Agent SDK)"
authors:
- Anthropic
organisation: Anthropic
source_type: docs
venue: Claude Agent SDK Docs
url: https://code.claude.com/docs/en/agent-sdk/permissions
year: 2026
date_published:
anthropic: true
topic:
- topic/claude-sdk
- topic/security
- topic/tool-use
tags:
- agent-sdk
- permissions
- cantusetool
- permission-modes
- subagents
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-docs
af_targets:
- af:DELEG-01
- af:RSCH-04/Q26
- af:ADR-0007
- af:ADR-0004
- cf:adapter/claude-code
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: aa08d0a8d63047be61085107d69edee11292ea2ebb35104890d938f401c4f273
---

# Configure permissions (Agent SDK)

> Anthropic, "Configure permissions", Claude Agent SDK Docs, undated (read 4 October 2026), https://code.claude.com/docs/en/agent-sdk/permissions.

## Summary

The page specifies how the Agent SDK decides whether a tool call runs. The SDK checks, in order: hooks, deny rules, ask rules, permission mode, allow rules, and finally the `canUseTool` callback. It also documents `allowed_tools` and `disallowed_tools`, six permission modes, dynamic mode changes during streaming sessions, and how subagents inherit the parent's mode.

## Key Concepts

- Six-step evaluation order; a hook deny, a deny rule and an ask rule apply even in `bypassPermissions`.
- `disallowed_tools=["Bash"]` removes the tool definition so the model cannot see it; `["Bash(rm *)"]` blocks matching calls in every mode.
- `allowed_tools` pre-approves tools and does not restrict `bypassPermissions`: with that mode every tool is approved.
- Auto-approved tools never reach `canUseTool`, so checks placed only there are bypassed.
- For a locked-down agent, pair an `allowedTools` list with `permissionMode: "dontAsk"`.

## Terminology

- `canUseTool`: callback consulted when no earlier step resolves a call.
- `permissionPrompts: 'none'`: TypeScript option that skips the callback; a `PermissionRequest` hook can still decide, otherwise the call is denied.
- Critical path: a location where `rm` and `rmdir` removals are never approved by an allow rule.

## Architecture and Implementation

Mode is set at query time with `permission_mode` or `permissionMode`, and changed mid-session with `set_permission_mode()` or `setPermissionMode()`. Allow rules accept tool-name globs only after a literal `mcp__<server>__` prefix. A subagent runs in the parent's mode unless its `AgentDefinition` sets one and the parent is in `default`, `dontAsk` or `plan`; `bypassPermissions` is never taken from the definition.

## Code Examples

```typescript
const options = {
  allowedTools: ["Read", "Glob", "Grep"],
  permissionMode: "dontAsk"
};
```

## Best Practices

- Use a `PreToolUse` hook for checks that must run on every call.
- Use `disallowed_tools` when `bypassPermissions` is needed but some tools must stay blocked.
- Set the mode explicitly, because omitting it can start in auto mode in current versions.
- Start restrictive and loosen with `setPermissionMode()` as trust builds.

## Warnings and Anti-Patterns

- A subagent can inherit `bypassPermissions` and gain full autonomous system access when the parent uses it.
- `bypassPermissions` fails to start as root outside a recognised sandbox on Linux and macOS.
- A bare `allowedTools` entry triggers the `CLAUDE_SDK_CAN_USE_TOOL_SHADOWED` warning when a callback is also set.

## Related Concepts

- [[claude-agent-sdk]]
- [[tool-use]]
- [[supervisor-worker-multi-agent]]

## Future Work

The source carries no roadmap.

## References

- https://code.claude.com/docs/en/agent-sdk/permissions
- https://code.claude.com/docs/en/agent-sdk/user-input
