---
type: source
status: draft
created: 2026-10-04
title: "Configure permissions (Claude Code)"
authors:
- Anthropic
organisation: Anthropic
source_type: docs
venue: Claude Code Docs
url: https://code.claude.com/docs/en/permissions
year: 2026
date_published:
anthropic: true
topic:
- topic/security
- topic/claude-code
- topic/best-practices
tags:
- claude-code
- permissions
- allow-deny-rules
- permission-modes
- governance
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-docs
af_targets:
- cf:adapter/claude-code
- af:ADR-0007
- af:RSCH-04/Q26
- af:RSCH-01/claude-code
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 6d0e9eb1c009a5507a07e387c5333b5bd2a0ebb1fe6cbc00a56e0cdaf698df0d
---

# Configure permissions (Claude Code)

> Anthropic, "Configure permissions", Claude Code Docs, undated (read 4 October 2026), https://code.claude.com/docs/en/permissions. Only the first part of the page (system, rule syntax, modes) was read in full.

## Summary

The page defines Claude Code's tiered permission system. Reads inside the working directory need no approval; Bash commands (outside a read-only set), file edits, web fetches (outside preapproved documentation domains) and web searches ask in Manual mode. Allow, ask and deny rules are evaluated in the order deny, then ask, then allow, and the first match wins regardless of specificity. Rules are enforced by Claude Code, not the model, so prompts and CLAUDE.md cannot change what is permitted. Six modes (`default`, `acceptEdits`, `plan`, `auto`, `dontAsk`, `bypassPermissions`) set the baseline.

## Key Concepts

- Rule format is `Tool` or `Tool(specifier)`. A bare deny such as `Bash` removes the tool from the model's context; a scoped deny such as `Bash(rm *)` leaves the tool and blocks matching calls.
- A broad deny beats a narrower allow; an allow cannot carve an exception out of a deny.
- Deny and ask rules can match a scalar input parameter with `Tool(param:value)`, for example `Agent(model:opus)`. The primary content field (Bash `command`, file paths, URLs) cannot be matched this way.
- `permissions.disableBypassPermissionsMode` and `permissions.disableAutoMode` can switch off those modes, most usefully in managed settings.
- "Don't ask again" approvals save to `.claude/settings.local.json` at the repository root.

## Terminology

- Manual mode: the CLI label for `default`.
- `dontAsk`: converts every prompt into a denial.
- Auto mode: a background classifier reviews actions instead of a person.
- Protected paths: locations such as `.git` and `.claude`.

## Architecture and Implementation

Permissions sit in settings files and are managed through `/permissions`, which shows each rule and its source file. Changes apply from the next tool call. Wildcards in Bash rules match any text including spaces, and everything before the first `*` is matched as written.

## Code Examples

```json
{
  "permissions": {
    "allow": ["Bash(npm run *)", "Bash(git commit *)"],
    "deny": ["Bash(git push *)"]
  }
}
```

## Best Practices

- Put the `*` after the subcommand, so `Bash(git log *)` allows only `git log`.
- Use `PreToolUse` hooks when a check must run on every call.
- Set managed settings for rules users must not override.
- Use `bypassPermissions` only in containers or VMs.

## Warnings and Anti-Patterns

- A push written as `git -C . push` is not matched by `Bash(git push *)`; the page points to a section on Bash rule limits.
- `bypassPermissions` skips prompts even for writes to protected paths.
- A wildcard before the subcommand, such as `Bash(git * main)`, triggers a startup warning.

## Related Concepts

- [[claude-code]]
- [[tool-use]]

## Future Work

The source carries no roadmap.

## References

- https://code.claude.com/docs/en/permissions
- https://code.claude.com/docs/en/permission-modes
