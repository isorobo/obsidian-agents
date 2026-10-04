---
type: meta
title: Agent-factory digest <YYYY-MM-DD>
status: review
created: <YYYY-MM-DD>
topic:
- topic/meta
tags:
- agent-factory
- digest
- wiki-agents
wiki_role: meta
---

# Agent-factory digest <YYYY-MM-DD>

> Period: notes first covered between <previous digest date, or "vault start"> and <YYYY-MM-DD>.
> One-way feed: this note is a reading list for agent-factory and code-factory. Nothing here is
> filed into either project; act on any item by choice. Target IDs are defined in
> [[99_Meta/agent-factory/af-targets|af-targets]].

## Summary counts

| measure | count |
|---|---|
| notes covered this digest | <n> |
| of which created this period | <n> |
| of which af-tagged this period (older notes) | <n> |
| tagged `none` | <n> |
| agent-factory IDs touched | <n> |
| code-factory IDs touched | <n> |
| RSCH-01 corpus items with at least one study note | <n> of 9 |
| RSCH-04 questions with at least one supporting note | <n> of 33 |

## By agent-factory target

(One `###` per `af:` ID that has at least one item this period, in af-targets.md order. Heading is
the ID and its gloss. One bullet per note: the wikilink, a colon, then one line on what this
changes or tests for agent-factory, grounded in the note. A note with several IDs appears under
each.)

### <af:ID> <gloss>

- [[10_Sources/<Folder>/<file-stem>|<Short Title>]]: <what this changes or tests for agent-factory>.

## Code-factory items

(One `###` per `cf:ADR-*` ID, and per `cf:adapter/*` ID for items that are not release notes.
Otherwise write "None this period.")

### <cf:ID> <gloss>

- [[10_Sources/<Folder>/<file-stem>|<Short Title>]]: <what this changes or tests for code-factory>.

## RSCH-01 coverage

(Cumulative over the whole vault. All 9 corpus items, in af-targets.md order. "present" when at
least one note carries the item's `af:RSCH-01/<item>` ID. For "missing", name the channel expected
to supply it.)

| corpus item | study notes present | status |
|---|---|---|
| 12-Factor Agents | <wikilinks or (none)> | <present or missing: expected from af-corpus-repos> |
| learn-agent-architecture | <...> | <...> |
| mini-SWE-agent | <...> | <...> |
| smolagents | <...> | <...> |
| ReAct | <...> | <...> |
| Reflexion | <...> | <...> |
| Generative Agents | <...> | <missing: expected from af-corpus-papers> |
| MCP | <...> | <...> |
| Claude Code | <...> | <...> |

## RSCH-04 coverage

<n> of 33 questions have at least one supporting note.

(Cumulative. All 33 rows. `notes` = count of notes carrying `af:RSCH-04/Qnn`; up to 3 example
wikilinks, newest first. Mark questions that gained a note this period with "(new)".)

| Q | question | notes | examples |
|---|---|---|---|
| Q01 | What is the minimum definition of an AI agent? | <n> | <wikilinks> |
| Q02 | What distinguishes an agent from an LLM call? | <n> | <wikilinks> |
| Q03 | What distinguishes an agent runtime from an agent definition? | <n> | <wikilinks> |
| Q04 | What should the Factory own? | <n> | <wikilinks> |
| Q05 | What should the model own? | <n> | <wikilinks> |
| Q06 | What should tools own? | <n> | <wikilinks> |
| Q07 | What should policy own? | <n> | <wikilinks> |
| Q08 | What should humans own? | <n> | <wikilinks> |
| Q09 | What state must be durable? | <n> | <wikilinks> |
| Q10 | What state must never be durable? | <n> | <wikilinks> |
| Q11 | What is memory? | <n> | <wikilinks> |
| Q12 | What is context? | <n> | <wikilinks> |
| Q13 | What is an observation? | <n> | <wikilinks> |
| Q14 | What is an action? | <n> | <wikilinks> |
| Q15 | What is a capability? | <n> | <wikilinks> |
| Q16 | What constitutes a tool? | <n> | <wikilinks> |
| Q17 | What constitutes delegation? | <n> | <wikilinks> |
| Q18 | What constitutes success? | <n> | <wikilinks> |
| Q19 | What constitutes evidence? | <n> | <wikilinks> |
| Q20 | What is the minimum useful evaluation architecture? | <n> | <wikilinks> |
| Q21 | What must survive a process crash? | <n> | <wikilinks> |
| Q22 | How should an agent resume? | <n> | <wikilinks> |
| Q23 | How should agents be isolated? | <n> | <wikilinks> |
| Q24 | How should agents communicate? | <n> | <wikilinks> |
| Q25 | What should a parent agent know about a child agent? | <n> | <wikilinks> |
| Q26 | How should permissions propagate? | <n> | <wikilinks> |
| Q27 | How should budgets propagate? | <n> | <wikilinks> |
| Q28 | How should human approval interact with execution? | <n> | <wikilinks> |
| Q29 | How should different models/runtimes be substituted? | <n> | <wikilinks> |
| Q30 | Which abstractions are genuinely universal? | <n> | <wikilinks> |
| Q31 | Which abstractions are merely implementation patterns? | <n> | <wikilinks> |
| Q32 | What should remain project-specific? | <n> | <wikilinks> |
| Q33 | What should remain outside Agent Factory entirely? | <n> | <wikilinks> |

## Suggested GSD todos

Paste any you want into agent-factory yourself. None is filed automatically, and none depends on
this vault: each cites primary sources only.

(At most 8. Order: missing RSCH-01 items with a primary source now in the vault; RSCH-04 questions
that gained evidence this period; adapter-affecting releases; ADR-relevant findings. Each is one
line in this form, with primary URLs and no wikilinks or vault paths.)

- `/gsd:add-todo <ID>: <action>. Primary: <url>[, <url>]. Focus: <what to extract or test>.`

## Release notes affecting adapters

(Release notes in this digest tagged `cf:adapter/*`, `af:REAL-02` or `af:ADR-0003`. Otherwise
write "None this period.")

| release | date | adapter | what changed for the adapter |
|---|---|---|---|
| [[10_Sources/Release-Notes/<file-stem>|<Product version>]] | <YYYY-MM-DD> | <cf:adapter/... or af:ID> | <flag, output format, permission, auth or API change, and whether the adapter recipe needs a check> |

## Notes covered

(Every note covered by this digest, including those tagged `none`, one per line, as a wikilink to
the vault-relative path without `.md`. The next digest reads this list to know what is already
covered. Never edit it by hand.)

- [[10_Sources/<Folder>/<file-stem>]]
