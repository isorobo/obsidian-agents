---
type: source
status: draft
created: 2026-10-04
title: "Intercept and control agent behavior with hooks (Agent SDK)"
authors:
- Anthropic
organisation: Anthropic
source_type: docs
venue: Claude Agent SDK Docs
url: https://code.claude.com/docs/en/agent-sdk/hooks
year: 2026
date_published:
anthropic: true
topic:
- topic/claude-sdk
- topic/security
- topic/observability
tags:
- agent-sdk
- hooks
- callbacks
- pretooluse
- audit
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-docs
af_targets:
- af:ADR-0004
- af:ADR-0007
- af:DELEG-01
- af:RSCH-04/Q26
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 048c1a560a1e0ef97a29d5c07fd9ba3098b32c539ea6b8f7be6936c6212a28d7
---

# Intercept and control agent behavior with hooks (Agent SDK)

> Anthropic, "Intercept and customize agent behavior with hooks", Claude Agent SDK Docs, undated (read 4 October 2026), https://code.claude.com/docs/en/agent-sdk/hooks.

## Summary

SDK hooks are callback functions that run application code on agent events such as a tool call, a tool result, a subagent start or stop, or session end. A callback receives the event input, a tool use ID and a context, and returns an output object that can allow, deny, defer or ask for a tool call, rewrite its input, add context, or stop the run. The page lists about thirty events and notes which exist only in the TypeScript SDK, then gives worked examples and troubleshooting for timeouts and matcher behaviour.

## Key Concepts

- Events include `PreToolUse`, `PostToolUse`, `PostToolUseFailure`, `Stop`, `SubagentStart`, `SubagentStop`, `PreCompact`, `PermissionRequest` and `Notification` in both SDKs; `SessionStart`, `SessionEnd` and many others are TypeScript only.
- Matchers test the tool name (`Write|Edit`, `^mcp__`); omitting the matcher runs the hook for every event of that type.
- Matching hooks run in parallel and the most restrictive result wins: deny, then defer, then ask, then allow.
- `updatedInput` must sit inside `hookSpecificOutput`; pair it with `allow` to auto-approve or `ask` to show the user.
- Async output (`async: true`) suits logging and webhooks, since it cannot block or modify.

## Terminology

- `HookMatcher`: Python wrapper pairing a matcher string with callbacks.
- `permissionDecisionReason`: text telling the model why a call was denied, so it does not retry.
- `systemMessage`: message shown to the user, not the model.

## Architecture and Implementation

Hooks come from `options.hooks` and from shell hooks in settings files when the relevant setting source is enabled. A hook deny applies even in `bypassPermissions` mode and runs before every other permission step. Timeouts default to 600 seconds for most events; a timed-out `PreToolUse` hook stops the tool call and tells the model the hook did not respond, and a timed-out `UserPromptSubmit` hook blocks the prompt rather than letting it through.

## Code Examples

```python
async def protect_env_files(input_data, tool_use_id, context):
    file_path = input_data["tool_input"].get("file_path", "")
    if file_path.split("/")[-1] == ".env":
        return {"hookSpecificOutput": {
            "hookEventName": input_data["hook_event_name"],
            "permissionDecision": "deny",
            "permissionDecisionReason": "Cannot modify .env files"}}
    return {}
```

## Best Practices

- Target hooks with a matcher and filter on `tool_input.file_path` inside the callback, since matchers see only tool names.
- Write each hook to act independently because completion order is not deterministic.
- Catch errors inside hooks (for example failed webhooks) instead of letting them propagate.
- Use `SubagentStop` hooks to track delegated work.

## Warnings and Anti-Patterns

- Hooks may not fire when the agent reaches `max_turns`.
- A `UserPromptSubmit` hook that spawns subagents can loop if the subagents trigger the same hook.
- Do not pair `updatedInput` with `defer`, which drops the modified input.
- Subagents multiply permission prompts unless hooks or inherited rules approve calls.

## Related Concepts

- [[claude-agent-sdk]]
- [[tool-use]]
- [[the-agent-loop]]

## Future Work

The source carries no roadmap.

## References

- https://code.claude.com/docs/en/agent-sdk/hooks
- https://code.claude.com/docs/en/hooks
