---
type: source
status: draft
created: 2026-10-04
title: "Anthropic Agent Skills Repository"
authors:
- Anthropic
organisation: Anthropic
source_type: repo
venue: GitHub
url: https://github.com/anthropics/skills
year: 2025
date_published: 2025-09-22
anthropic: true
topic:
- topic/agent-skills
- topic/best-practices
tags:
- skills
- skill-md
- plugins
- spec
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-github
af_targets:
- cf:ADR-0012
- cf:ADR-0011
- af:RSCH-01/claude-code
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 21b837a7069a8092d29bc04eb392993fe25a2c3bac6465377d660746bbc0ac20
---

# Anthropic Agent Skills Repository

> Anthropic, "Anthropic Agent Skills Repository", GitHub (anthropics), repository created 22 September 2025, https://github.com/anthropics/skills.

## Summary

The public repository for Agent Skills: folders of instructions, scripts and resources that Claude loads dynamically to improve performance on specialised tasks. The layout has three parts: `./skills` with examples across creative design, development, enterprise communication and document handling; `./spec` with the Agent Skills specification; and `./template` as a starter. The README describes skills as demonstration and educational material, and says behaviour may differ from Claude's actual capabilities, so users must test in their own environment.

## Key Concepts

- A skill is a folder whose `SKILL.md` has YAML frontmatter with two mandatory fields: `name` (unique, lowercase, hyphens) and `description` (what it does and when to use it).
- The markdown body holds the instructions, examples and guidelines Claude follows once the skill activates.
- Use across surfaces: Claude Code (register with `/plugin marketplace add anthropics/skills`, then install sets such as document-skills or example-skills), Claude.ai for paid users, and the Claude API through the Skills API.

## Terminology

- Skill: a packaged capability folder with a `SKILL.md`.
- Marketplace: a plugin source registered in Claude Code.

## Architecture and Implementation

Skills are file-based, so they are versionable and portable across the three surfaces. The description field is what lets the model decide when to activate a skill.

## Code Examples

The README shows no code beyond the slash command `/plugin marketplace add anthropics/skills`.

## Best Practices

- Write a precise description, since it drives activation.
- Start from the template folder.
- Test skills thoroughly before relying on them.

## Warnings and Anti-Patterns

- Most skills are Apache 2.0, but the DOCX, PDF, PPTX and XLSX skills are source-available, not open source.
- The skills are demonstrations, not production guarantees.

## Related Concepts

- [[claude-code]]
- [[prompt-engineering]]
- [[tool-use]]

## Future Work

None stated; the specification lives in `./spec`, which was not fetched here.

## References

- https://github.com/anthropics/skills
