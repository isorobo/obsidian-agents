---
type: source
status: draft
created: 2026-10-04
title: "Claude Code Hooks Reference"
authors:
- Anthropic
organisation: Anthropic
source_type: docs
venue: Claude Code Docs
url: https://code.claude.com/docs/en/hooks
year: 2026
date_published:
anthropic: true
topic:
- topic/claude-code
- topic/security
- topic/tool-use
tags:
- claude-code
- hooks
- pretooluse
- lifecycle
- policy
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-docs
af_targets:
- cf:adapter/claude-code
- af:RSCH-01/claude-code
- af:ADR-0007
- af:ADR-0004
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 0a2d389b11ab8532298d8d2edb414d9990ed2fa26f9ff0d74d045c110c90cc6b
---

# Claude Code Hooks Reference

> Anthropic, "Claude Code Hooks Reference", Claude Code Docs, undated (read 4 October 2026), https://code.claude.com/docs/en/hooks. The page was read through a summarising fetch, so details are condensed.

## Summary

Hooks are user-defined commands, HTTP endpoints, MCP tools, prompts or subagents that run automatically at points in the Claude Code lifecycle. They fire per session (`SessionStart`, `SessionEnd`), per turn (`UserPromptSubmit`, `Stop`, `StopFailure`) and per tool call (`PreToolUse`, `PostToolUse`). Configuration nests three levels: event, matcher, hook list. Hooks can observe, block, modify input or output, or inject context, making them the deterministic control layer around a probabilistic model.

## Key Concepts

- Five hook types: `command`, `http`, `mcp_tool`, `prompt`, `agent` (experimental).
- Locations: user settings, project settings, local project settings, managed policy, plugin `hooks/hooks.json`, and skill or subagent frontmatter.
- Matchers filter on tool name (`Bash`, `Edit|Write`, regex such as `^mcp__`), session source, notification type or agent type. The `if` field filters further with permission rule syntax.
- Exit code 0 means success (JSON parsed), 2 is a blocking error on events such as `PreToolUse`, `UserPromptSubmit` and `Stop`, and other codes do not block.
- `PreToolUse` decisions: `allow`, `deny`, `ask` or `defer`, with `updatedInput` to rewrite arguments.

## Terminology

- Exec form: a command with `args` set, spawned without a shell.
- Shell form: a command string passed to a shell.
- `hookSpecificOutput`: JSON object carrying per-event decisions.
- `additionalContext`: text injected for the model.

## Architecture and Implementation

Every hook receives JSON on stdin with `session_id`, `transcript_path`, `cwd`, `permission_mode`, `hook_event_name` and event-specific fields. Defaults for `timeout` are 600 seconds for command, http and mcp_tool hooks, 30 for prompt hooks and 60 for agent hooks. Path placeholders include `${CLAUDE_PROJECT_DIR}` and `${CLAUDE_PLUGIN_ROOT}`. Hooks from untrusted project settings need workspace trust before they run; user, plugin and managed hooks are exempt.

## Code Examples

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          { "type": "command", "if": "Bash(rm *)", "command": "${CLAUDE_PROJECT_DIR}/.claude/hooks/block-rm.sh", "args": [] }
        ]
      }
    ]
  }
}
```

## Best Practices

- Put hard policy (blocking destructive commands, protecting files) in `PreToolUse` hooks, not in prompts.
- Prefer exec form with `args` to avoid shell interpretation.
- Use `--debug-file` to see hook timing, input and output.
- Keep managed hooks in managed settings, since users cannot disable them.

## Warnings and Anti-Patterns

- Exit code 2 is ignored on observational events such as `Notification` and `SessionEnd`.
- `disableAllHooks` can turn hooks off in user settings, so policy that must hold belongs in managed settings.
- Project hooks run unprompted under non-interactive `-p` unless bare mode is used.

## Related Concepts

- [[claude-code]]
- [[tool-use]]
- [[claude-agent-sdk]]

## Future Work

The source carries no roadmap; the agent hook type is marked experimental.

## References

- https://code.claude.com/docs/en/hooks
- https://code.claude.com/docs/en/hooks-guide
