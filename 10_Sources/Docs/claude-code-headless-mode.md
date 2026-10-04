---
type: source
status: draft
created: 2026-10-04
title: "Run Claude Code programmatically"
authors:
- Anthropic
organisation: Anthropic
source_type: docs
venue: Claude Code Docs
url: https://code.claude.com/docs/en/headless
year: 2026
date_published:
anthropic: true
topic:
- topic/claude-code
- topic/deployment
- topic/best-practices
tags:
- claude-code
- headless
- print-mode
- stream-json
- ci
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-docs
af_targets:
- cf:adapter/claude-code
- af:RSCH-01/claude-code
- af:BI-13
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 88001ed5bfe71d7c8c357adc65451aef49d5d621bc66e7b8b5ca1cae169aa2a4
---

# Run Claude Code programmatically

> Anthropic, "Run Claude Code programmatically", Claude Code Docs, undated (read 4 October 2026), https://code.claude.com/docs/en/headless.

## Summary

The page documents non-interactive use of Claude Code through `claude -p`, described as the Agent SDK exposed as a CLI. It covers exit codes, `--bare` mode (skips auto-discovery of hooks, skills, plugins, MCP servers, auto memory and CLAUDE.md, and is recommended for scripted calls), output formats (`text`, `json`, `stream-json`), schema-constrained output with `--json-schema`, session continuation with `--continue` and `--resume`, auto-approval through `--allowedTools` and permission modes, and `--permission-prompts none` for unattended runs. It also specifies shutdown behaviour (SIGTERM exits with 143, background tasks and subagents at exit) and the `system/init` event fields a CI gate can check.

## Key Concepts

- `claude -p` runs one prompt and exits with code 0 on success, non-zero on failure; in-run failures such as missing auth print as the result on stdout.
- `--bare` gives the same result on every machine because it ignores host hooks, plugins, MCP config and CLAUDE.md; context is passed by flags (`--settings`, `--mcp-config`, `--agents`, `--append-system-prompt`).
- `--output-format json` returns result, session ID, cost (`total_cost_usd`) and metadata; with `--json-schema` the structured answer appears in `structured_output`.
- `stream-json` with `--verbose` emits newline-delimited events; the last line is a `result` message. Subagent messages carry `parent_tool_use_id`.
- Permission baselines: `--allowedTools` rules, or `--permission-mode` of `auto`, `dontAsk` or `acceptEdits`.

## Terminology

- Bare mode: startup mode that skips auto-discovery of local configuration.
- `dontAsk`: permission mode that denies every call that would otherwise prompt.
- `permission_denials`: list in the final result message of calls that were denied.
- `system/init`: first stream event, listing model, tools, MCP servers, plugins and error arrays.

## Architecture and Implementation

Sessions are stored and resumable by ID or by transcript path, across directories on one machine. Piped stdin is capped at 10MB. A `-p` session without `--bare` runs project hooks and connects project MCP servers even in an untrusted folder, with no trust dialog. `system/init` exposes `plugin_errors` and `mcp_server_errors`, which a CI step can fail on. The `capabilities` array supports feature detection instead of version comparison. API retries surface as `system/api_retry` events.

## Code Examples

```bash
claude -p "Run the test suite and fix any failures" --allowedTools "Bash,Read,Edit"
claude -p "Summarize this project" --output-format json | jq -r '.result'
session_id=$(claude -p "Start a review" --output-format json | jq -r '.session_id')
claude -p "Continue that review" --resume "$session_id"
```

## Best Practices

- Use `--bare` in CI and scripts so host configuration cannot change behaviour.
- Scope Bash rules by subcommand, for example `Bash(git diff *)`, rather than allowing all of Bash.
- Pass `--permission-prompts none` with `--permission-mode auto` when nobody can answer prompts.
- Check `plugin_errors` and `mcp_server_errors` in `system/init`, because invalid config is skipped without a failing exit.
- Send SIGINT or call `interrupt()` before stopping a process if the turn should end cleanly.

## Warnings and Anti-Patterns

- Without `--bare`, repository hooks and MCP servers run under `-p` with no trust prompt.
- SIGTERM leaves the interrupted turn unfinished and records no result for it.
- Cost figures are client-side estimates and can differ from the bill.
- A bare `Bash` allow entry is dropped when a run starts in auto mode.

## Related Concepts

- [[claude-code]]
- [[claude-agent-sdk]]
- [[tool-use]]

## Future Work

The page says `--bare` will become the default for `-p` in a future release.

## References

- https://code.claude.com/docs/en/headless
- https://code.claude.com/docs/en/cli-reference
