---
type: source
status: draft
created: 2026-07-11
title: "Anthropic's 300+ Claude Code Skills: Lessons Learned"
authors:
- Jason Zhou
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 3.4
url: https://www.aibuilderclub.com/blog/agent-skills-best-practices-guide
year: 2026
date_published: 2026-06-09
anthropic: true
topic:
- topic/best-practices
- topic/agent-skills
tags:
- agent-skills
- claude-code
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
---

# Anthropic's 300+ Claude Code Skills: Lessons Learned

> Jason Zhou, "Anthropic's 300+ Claude Code Skills: Lessons Learned", AI Builder Club, Build AI Agents Course, 9 June 2026, https://www.aibuilderclub.com/blog/agent-skills-best-practices-guide.

Course listing note: the course index labels this lesson "3.4 — Why MCP is Dead & Skills Replace It", but the article at this URL is Anthropic's internal Skills playbook, not an MCP-obituary piece. Filed under its actual published title and content.

## Summary

Anthropic runs several hundred Agent Skills internally; the author, running 26 across two of his own projects, distils the internal playbook into what a Skill actually is (a self-contained folder, not a single Markdown file), nine functional types worth building, and the structural and description choices that determine whether a Skill fires reliably or sits unused. The single most load-bearing claim: the folder itself, not any one document inside it, is the context-engineering surface.

## Key Concepts

- A Skill is a folder — instructions, scripts, and reference material together — that Claude Code discovers and loads automatically; the folder is the unit of design, not any file within it.
- Nine functional Skill types: library/API reference, product verification, data fetching/analysis, business-process automation, code scaffolding/templates (the most common), code quality/review, CI/CD and deploy, runbooks, and infrastructure ops. Anthropic identifies verification Skills as delivering the largest quality improvement to output.
- Progressive disclosure through the file system: decision-critical instructions live in `SKILL.md` (always loaded); detailed reference material lives in `references/`/`templates/` subfolders, loaded only on demand.
- A Skill's `description` field is a trigger signal read by the model to decide whether to fire the Skill, not documentation for a human reader — the phrase "Use when the user wants to..." plus explicit trigger phrases determines invocation reliability far more than a general description does.
- A "gotchas" list — where the model reliably fails or where a default assumption is wrong for this specific domain — is named as the highest-value section a Skill can carry.

## Terminology

- Skill (Anthropic sense) — a self-contained folder of instructions, scripts, and reference material that an agent discovers and loads, distinct from a single instructional document.
- Progressive disclosure — loading only the always-needed instructions upfront (`SKILL.md`) and pulling detailed reference material in on demand from subfolders.
- Trigger signal — the function a Skill's description field performs: telling the model when to fire the Skill, not explaining the Skill to a person.

## Architecture and Implementation

Two worked folder shapes: a simple Skill (a single 15-line `SKILL.md`) and a complex one (a 274-line `SKILL.md` plus a `references/` subfolder of templates and patterns). Skills can register hooks scoped to their own invocation — a `/careful` mode blocking destructive operations (`rm -rf`, `DROP TABLE`, force-push) via a `PreToolUse` hook, or a `/freeze` mode restricting edits to specified directories during debugging. Measurement runs through the same `PreToolUse` hook mechanism, logging every invocation's timestamp, Skill name, and session ID; a low trigger rate points to a description problem, while bad output despite firing points to a missing gotcha or unclear instruction.

## Code Examples

No runnable code; the lesson works at the level of folder structure, `SKILL.md` content patterns, and hook configuration rather than a single program.

## Best Practices

- Fit a Skill to exactly one of the nine types; a Skill spanning multiple categories confuses the model about when to use it.
- Write descriptions as trigger phrases matching how a user actually asks, not as a neutral summary of what the Skill does.
- Put a gotchas list in every Skill that has one; it is the section most likely to prevent a repeated, domain-specific failure.
- Prefer rules and principles over rigid, over-constrained step-by-step procedures, which reduce the model's ability to adapt.
- Give a Skill memory by having it write an append-only log inside its own folder, read back on the next invocation.

## Warnings and Anti-Patterns

- Repeating information the model already knows wastes the Skill's context budget for no benefit.
- Cramming everything into one Markdown file forfeits the entire point of progressive disclosure.
- Writing a description for a human reader, rather than as a trigger signal, is the single most common reason a Skill goes unused.
- MCP has no native Skill-to-Skill dependency mechanism; referencing another Skill by name in `SKILL.md` invokes it only if present, and fails silently if it is not.

## Related Concepts

- [[best-practices-index]]
- [[claude-code]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson announces a companion video walkthrough of the same playbook but the fetched page carries no transcript or show notes for it — a gap worth revisiting on a future pass.

## References

- Anthropic's 300+ Claude Code Skills: Lessons Learned — https://www.aibuilderclub.com/blog/agent-skills-best-practices-guide
