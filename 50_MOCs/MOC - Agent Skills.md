---
type: moc
status: draft
created: 2026-07-11
name: Agent Skills
topic:
- topic/agent-skills
tags: []
wiki_role: moc
---

# MOC - Agent Skills

> The Agent Skills pattern itself — folder format, authoring, distribution, and installation — across Anthropic's own playbook and the wider third-party ecosystem.

## Start Here

- [[10_Sources/Blog/agent-skills-best-practices|Anthropic's 300+ Claude Code Skills: Lessons Learned]] — the format's own origin and best-practice baseline.

## Core Notes

Curated wikilinks, grouped by sub-theme.

- Official libraries: [[10_Sources/Blog/google-skills-official-library|google/skills]]
- Community libraries: [[10_Sources/Blog/last30days-real-time-research-skill|last30days-skill]], [[10_Sources/Repos/davidondrej-skills|davidondrej/skills]]
- Worked examples from `anthropics/skills` itself: [[10_Sources/Docs/mcp-builder-skill|MCP Builder]], [[10_Sources/Docs/claude-api-skill|Claude API Skill]]

## All Notes in This Topic

```dataview
LIST
FROM ""
WHERE contains(topic, "topic/agent-skills") AND type != "moc"
SORT file.name ASC
```

## Related Maps

- [[MOC - Tool Use]]
- [[MOC - Best Practices]]
- [[MOC - Claude Code]]
- [[MOC - Home]]
