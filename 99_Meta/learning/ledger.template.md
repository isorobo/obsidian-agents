---
type: ledger
title: Concept Ledger Template
status: permanent
created: 2026-08-13
topic:
- topic/learning
- topic/foundations
tags: []
wiki_role: meta
---

# Concept Ledger Template

Seed file. Copy this to `99_Meta/learning/ledger.md` before first use:

```
cp "99_Meta/learning/ledger.template.md" "99_Meta/learning/ledger.md"
```

The live ledger is gitignored. It holds one operator's learning state, which
is private. This template holds the schema and the seed rows, which are not.
`CLAUDE.md` loads `ledger.md`, not this file. Without the copy, the kernel
loads a missing file and standing rule 1 has nothing to read.

Replace the reading order below with your own. The rows are the vault's
Canonical Reading Order in [[00_Home/index|Home]]. Keep the columns.

Status advances on evidence, never on reading:

| Status | Evidence required |
|---|---|
| `not-started` | Default. |
| `explained` | Claude taught it and the learner restated it in his own words. |
| `applied` | The learner built something that uses it. |
| `debugged` | The learner fixed a failure caused by it. |
| `taught-back` | The learner explained it without help. |

Standing rule 1 reads this table. A concept at `not-started` is off limits as
a solution unless it is the stated learning objective. A project may reorder
the queue. A project may not skip the gate.

| # | Concept | Status | Evidence | Last touched | Open question |
|---|---|---|---|---|---|
| 1 | [[what-is-an-ai-agent]] | not-started | | | |
| 2 | [[agent-vs-llm]] | not-started | | | |
| 3 | [[the-agent-loop]] | not-started | | | |
| 4 | [[tool-use]] | not-started | | | |
| 5 | [[memory]] | not-started | | | |
| 6 | [[planning-and-reasoning]] | not-started | | | |
| 7 | [[prompt-engineering]] | not-started | | | |
| 8 | [[react]] | not-started | | | |
| 9 | [[plan-and-execute]] | not-started | | | |
| 10 | [[reflexion]] | not-started | | | |
| 11 | [[mcp]] | not-started | | | |
| 12 | [[claude-agent-sdk]] | not-started | | | |
| 13 | [[claude-code]] | not-started | | | |
| 14 | [[supervisor-worker-multi-agent]] | not-started | | | |
| 15 | [[workflow-vs-autonomous-agent]] | not-started | | | |
| 16 | [[evaluation]] | not-started | | | |
| 17 | [[best-practices-index]] | not-started | | | |
| 18 | [[anti-patterns-index]] | not-started | | | |

## Writing to the live ledger

Claude proposes rows and never writes them silently. `/ledger` shows the
current state and asks before it edits. `/close` batches a session's changes
into one approval. Every response carries a ledger stamp naming the concept it
touched and the status it would set.

## See also

- [[99_Meta/learning/README|How the learning system works]]
- [[99_Meta/learning/failure-log|Failure log]]
- [[MOC - Meta]]
