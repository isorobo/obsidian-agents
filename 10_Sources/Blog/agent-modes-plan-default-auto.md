---
type: source
status: draft
created: 2026-10-04
title: "Plan vs Default vs Auto Mode: Coding Agent Trust Levels"
authors:
- Shirley
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club - Build AI Agents Course, Section 4.1
url: https://www.aibuilderclub.com/blog/agent-modes-plan-default-auto
year: 2026
date_published: 2026-06-11
anthropic: false
topic:
- topic/security
- topic/claude-code
tags:
- permission-modes
- approval-fatigue
- auto-mode
- trust-levels
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
af_targets:
- af:ADR-0007
- af:RSCH-04/Q28
- af:RSCH-04/Q26
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: abb6d9c23b2bca2a7104106fef3d34b5fb24daaa337d4b5a586ef3a956890ddf
---

# Plan vs Default vs Auto Mode: Coding Agent Trust Levels

> Shirley, "Plan vs Default vs Auto Mode: Coding Agent Trust Levels", AI Builder Club, Build AI Agents Course, 11 June 2026, https://www.aibuilderclub.com/blog/agent-modes-plan-default-auto.

## Summary

The lesson frames coding-agent permission modes as three trust levels and a gear-shifting workflow. Plan is read-only and outputs a markdown plan. Default allows reads and asks before writes or commands. Auto runs autonomously with a safety classifier watching. The central tension is autonomy against risk: too many prompts train users to approve blindly, which the author says is worse than fewer, better-placed checks.

## Key Concepts

- Plan mode suits unfamiliar codebases and structural changes.
- Default mode suits feature work and production-adjacent code.
- Auto mode suits mechanical tasks, isolated environments and agent-team runs.
- Claude Code's auto mode uses a second model as classifier. Safe actions pass silently, risky ones (forced pushes, credential leaks) are intercepted, and 3 consecutive or 20 cumulative blocks return the session to manual approval. Paths such as `.git` and `.env` stay approval-gated. The lesson notes it is a research preview.
- Suggested sequence: Plan, then Auto for mechanical work, then Default for sensitive code, then full review.

## Terminology

- Approval fatigue: reflexive approval after repeated dialogs.
- Blast radius: scope of damage from a wrong action.
- Gear-shifting: switching modes by task risk.

## Architecture and Implementation

Per-tool granularity is shown with an OpenCode permission config.

## Code Examples

```json
{ "permission": { "bash": { "git status*": "allow", "rm *": "deny", "*": "ask" } } }
```

## Best Practices

- Plan first: reviewing a plan is cheaper than reverting a failed attempt.
- Configure per-tool rules, not all-or-nothing trust.
- Use Auto in sandboxes, worktrees or experimental branches.

## Warnings and Anti-Patterns

- Treating modes as fixed personalities.
- Skipping Plan on major refactors to save time.
- A global allow-all permission.
- Using any automation mode to replace architectural review.

## Related Concepts

- [[claude-code]]
- [[tool-use]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The auto-mode classifier is still labelled a research preview; the lesson points to OS-level sandboxing as the complement.

## References

- Plan vs Default vs Auto Mode: https://www.aibuilderclub.com/blog/agent-modes-plan-default-auto
- Cited by the lesson: OpenCode permission docs; Armin Ronacher on Plan mode; Anthropic documentation on approval fatigue.
