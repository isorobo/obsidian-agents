---
type: source
status: draft
created: 2026-07-11
title: "Claude API Skill - API Reference Guidance for Claude"
authors:
- Anthropic
organisation: claudeskills.org (mirrors anthropics/skills, Anthropic)
source_type: docs
venue: claudeskills.org
url: https://www.claudeskills.org/docs/skills-cases/claude-api
year: 2026
date_published: 2026-07-01
anthropic: true
topic:
- topic/claude-sdk
- topic/agent-skills
tags:
- agent-skills
- claude-api
nlm_id:
nlm_skip: false
watchlist_channel:
---

# Claude API Skill - API Reference Guidance for Claude

> Anthropic, "Claude API Skill - API Reference Guidance for Claude", claudeskills.org (content adapted from `anthropics/skills`, MIT licence), last synced 8 July 2026 against the 1 July 2026 upstream, https://www.claudeskills.org/docs/skills-cases/claude-api.

## Summary

An official Anthropic Agent Skill built to solve a specific, self-referential problem: a model's own training knowledge of its API goes stale, since model identifiers, pricing, and SDK usage patterns keep changing after training data is frozen. The skill keeps that reference material current outside the model's weights, so Claude can look up today's answer instead of recalling a possibly outdated one from training.

## Key Concepts

- Model knowledge decay is named explicitly as the problem: "models' training knowledge of their own API goes stale," and the fix is an externally maintained, continuously updated reference the model reads rather than recalls.
- The `SKILL.md` file itself functions as a router (roughly 73KB), holding default output requirements, a decision tree for choosing between the Messages API, Tool Runner, Managed Agents, and the Agent SDK, a dated model table (cached 24 June 2026), and authentication guidance — then dispatching to per-language reference packs for the actual detail.
- Five language-specific reference packs (curl, Python, TypeScript, Go, C#) cover streaming, tool use, batches, the files API, and managed agents, each kept as focused files rather than folded into the router.
- Explicit date-stamping of cached information (the model table's 24 June 2026 cache date is stated directly in the file) is the skill's own stated design practice for making its own currency transparent to a reader or a debugging session.

## Terminology

- Router pattern (Skill sense) — a `SKILL.md` that itself makes a small number of high-level decisions (which API surface to use) and then dispatches to separate, focused reference files for implementation detail, rather than holding everything in one document.
- Model knowledge decay — the specific failure mode this skill targets: a model's own training-time knowledge of API identifiers, pricing, or usage patterns becoming outdated as the API evolves after training.

## Architecture and Implementation

The skill folder holds the primary `SKILL.md` router, per-language directories (curl, Python, TypeScript, Go, C#) with the detailed reference content, and licensing documentation. The repository location is given directly: `skills/claude-api` inside `anthropics/skills`.

## Code Examples

None reproduced in the fetched summary; the per-language reference packs contain the actual code guidance, not shown in full here.

## Best Practices

- Date-stamp cached reference data explicitly, so a reader (human or model) can judge its own currency rather than trusting it blindly.
- Use a router-plus-per-language-file architecture for a large reference knowledge base, rather than one combined document covering every language and API surface at once.
- Route API-surface decisions (Messages API versus Tool Runner versus Managed Agents versus Agent SDK) through an explicit decision tree rather than leaving the choice implicit.

## Warnings and Anti-Patterns

None stated in the content retrieved beyond the core problem statement — a model trusting its own stale training-time knowledge of the API over the skill's maintained reference.

## Related Concepts

- [[claude-agent-sdk]]
- [[claude-code]]
- [[10_Sources/Blog/agent-skills-best-practices|Anthropic's 300+ Claude Code Skills: Lessons Learned]]
- [[10_Sources/Docs/mcp-builder-skill|MCP Builder - Claude Skill for Building MCP Servers]]

## Future Work

The fetched page summarises the router structure without reproducing the actual model table, pricing figures, or per-language code samples; those would need a direct read of the `anthropics/skills` repository to capture accurately, and would go stale quickly given the skill's own stated purpose.

## References

- Claude API Skill - API Reference Guidance for Claude — https://www.claudeskills.org/docs/skills-cases/claude-api
- Upstream source: `anthropics/skills`, `skills/claude-api` (MIT licence)
