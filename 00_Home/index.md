---
type: meta
title: Home
status: permanent
created: 2026-07-10
topic:
- topic/meta
tags: []
wiki_role: index
---

# wiki-agents

A knowledge base on AI Agents. The Anthropic ecosystem is the primary lens;
broader agentic AI provides context. The vault carries the reader from beginner
to advanced practitioner.

## Navigate

- [[MOC - Home]] — every topic map.
- [[99_Meta/schema.md|Schema]] — the metadata contract.
- [[99_Meta/roadmap.md|Roadmap]] — how the vault grows.

## Canonical Reading Order

Read in this order to progress from foundations to practice.

1. [[what-is-an-ai-agent]]
2. [[agent-vs-llm]]
3. [[the-agent-loop]]
4. [[tool-use]]
5. [[memory]]
6. [[planning-and-reasoning]]
7. [[prompt-engineering]]
8. [[react]]
9. [[plan-and-execute]]
10. [[reflexion]]
11. [[mcp]]
12. [[claude-agent-sdk]]
13. [[claude-code]]
14. [[supervisor-worker-multi-agent]]
15. [[workflow-vs-autonomous-agent]]
16. [[evaluation]]
17. [[best-practices-index]]
18. [[anti-patterns-index]]

## Vault Dashboard

### Stubs awaiting enrichment

```dataview
LIST
FROM ""
WHERE status = "stub"
SORT file.mtime DESC
```

### Added in the last 7 days

```dataview
LIST
FROM ""
WHERE file.cday >= date(today) - dur(7 days)
SORT file.cday DESC
```

### All concepts

```dataview
TABLE topic, status
FROM ""
WHERE type = "concept" OR type = "architecture"
SORT file.name ASC
```
