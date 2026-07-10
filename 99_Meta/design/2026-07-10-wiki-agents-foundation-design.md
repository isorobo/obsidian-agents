---
type: meta
title: wiki-agents Foundation — Design Specification
status: draft
created: 2026-07-10
topic:
- topic/meta
wiki_role: meta
---

# wiki-agents Foundation — Design Specification

Design for the foundation of **wiki-agents**, an Obsidian knowledge vault on AI
Agents with the Anthropic ecosystem as the primary lens. This document is the
approved design. It governs the first build pass and hands to an execution plan.

Vault path: `C:\Users\Simon\Documents\wiki-agents`.

---

## 1. Purpose and Desired End State

The vault answers questions across the full agent lifecycle: what an agent is,
how it differs from a language model, how agents are designed, built, deployed,
monitored, evaluated, and maintained, which patterns work, which fail, and where
the field heads. It carries a beginner-to-advanced reading path and prioritises
the Anthropic ecosystem while documenting broader agentic AI for context.

**Desired end state of this pass.** A working vault holds:

- Eleven functional folders and their `.gitkeep` or index notes.
- A controlled metadata schema in `99_Meta/schema.md`.
- Nine templates in `90_Templates/`.
- Twenty-three MOCs: one Home MOC plus twenty-two topic MOCs.
- Twenty-two seed notes, each grounded in live primary sources.
- A research pipeline: watchlist, monitor design, four workflows.
- Integration docs: plugins, Dataview, Tasks, Mermaid library, roadmap.

**How to verify.** Section 17 lists split success criteria. Every automated
criterion names a command. Every manual criterion names a human check.

---

## 2. What This Pass Will Not Do

- Populate the full corpus. Content beyond the twenty-two seed notes grows
  through later research runs.
- Extract the complete Boris Cherny body of work. This pass creates a profile
  stub and one worked source; a dedicated run builds the full extraction.
- Build the full Anthropic release chronology. This pass creates one release
  note in the ingestion format as the exemplar.
- Write the monitor subagent as executable code. This pass specifies the monitor
  and wires its state and watchlist; a later pass registers the subagent.
- Install Obsidian plugins. This pass recommends plugins and writes the queries
  that depend on them.
- Modify the sibling vaults `wiki-tokenise`, `wiki-ai-thinkers`, or `wiki-law`.

---

## 3. Taxonomy Decision

The vault uses a **hybrid taxonomy**: a stable functional folder spine plus a
controlled `topic` vocabulary expressed through MOCs and tags.

Rationale. The stated goal is a base that accumulates rather than fragments.
Rigid topical folders fragment: a note on MCP security belongs to security,
tool use, and MCP at once, so a folder forces a false single home. Folders sort
by kind. MOCs and tags sort by topic. Dataview rebuilds any topical view on
demand. This choice also matches the proven `wiki-tokenise` pattern, so the
research pipeline and NotebookLM bridge transfer without rework.

Evidence for the proven pattern: `wiki-tokenise/99_Meta/schema.md:33` defines
the functional-folder plus controlled-vocabulary approach this design adapts.

---

## 4. Folder Structure

| Folder | Purpose |
|---|---|
| `00_Home/` | Vault entry hub and canonical reading order. |
| `00_Inbox/` | Unprocessed captures awaiting triage. |
| `10_Sources/` | One note per primary source, grouped by source-type subfolder. |
| `10_Sources/PDFs/` | Raw binary downloads. Excluded from version control. |
| `10_Sources/NotebookLM-Exports/` | NotebookLM audio, brief, and slide artefacts. |
| `20_People/<slug>/` | One folder per person or organisation. Holds `profile.md`. |
| `30_Concepts/` | Atomic concept and architecture notes. |
| `40_Guides/` | Implementation guides, engineering guides, tutorials, code examples. |
| `50_MOCs/` | Maps of Content. One Home MOC and twenty-two topic MOCs. |
| `60_Drafts/` | Work-in-progress essays and deep-research outputs. |
| `70_Research/` | Active research threads. One folder per thread. |
| `80_Attachments/` | Images, diagrams, Mermaid source. |
| `90_Templates/` | Templater-compatible templates. |
| `99_Meta/` | Schema, design docs, watchlist, pipeline state, integration docs. |

Anti-patterns, best practices, patterns, and release notes live as note `type`
values inside `30_Concepts/` and `10_Sources/`, surfaced through their MOCs.
They do not take dedicated folders.

---

## 5. Naming Conventions

- Concept and guide files: kebab-case slug, `what-is-an-ai-agent.md`.
- MOC files: `MOC - <Topic Name>.md`, title case after the prefix.
- People and organisations: `20_People/<slug>/profile.md`, slug in kebab-case.
- Sources: `10_Sources/<Source-Type>/<slug>.md`.
- Release notes: `10_Sources/Release-Notes/<product>-<yyyy-mm-dd>.md`.
- No spaces in slugs. Display titles carry spaces through frontmatter `title`.
- One concept per file. A file names one idea.

---

## 6. Metadata Schema

`99_Meta/schema.md` holds the controlled vocabulary. Every note conforms. A new
value requires a schema update before use.

### 6.1 Required on every note

| Field | Values | Notes |
|---|---|---|
| `type` | see 6.2 | Governs the template. |
| `status` | `inbox`, `stub`, `draft`, `review`, `permanent`, `archived` | Lifecycle state. |
| `created` | ISO date | Creation date. |
| `topic` | list from 6.3 | Controlled topic vocabulary. |
| `tags` | list of free strings | Open folksonomy. |

### 6.2 `type` enum

`concept`, `architecture`, `pattern`, `anti-pattern`, `guide`, `source`,
`person`, `organisation`, `release`, `moc`, `draft`, `glossary`, `meta`.

### 6.3 `topic` controlled vocabulary (22)

`topic/foundations`, `topic/concepts`, `topic/architectures`,
`topic/claude-sdk`, `topic/claude-code`, `topic/mcp`, `topic/tool-use`,
`topic/memory`, `topic/planning`, `topic/prompt-engineering`,
`topic/agent-patterns`, `topic/multi-agent`, `topic/deployment`,
`topic/observability`, `topic/evaluation`, `topic/security`,
`topic/best-practices`, `topic/anti-patterns`, `topic/release-notes`,
`topic/boris-cherny`, `topic/research-papers`, `topic/meta`.

### 6.4 Source notes

| Field | Values | Notes |
|---|---|---|
| `title` | free string | Work title. |
| `authors` | list of strings | Author names. |
| `organisation` | free string | Issuing body, for example `Anthropic`. |
| `source_type` | `docs`, `blog`, `paper`, `talk`, `repo`, `changelog`, `release-note`, `interview`, `sdk-reference`, `book`, `tutorial` | Required. |
| `url` | URL | Canonical link. `TBD` permitted at stub stage. |
| `year` | integer | Publication year. |
| `date_published` | ISO date | Where day-granularity matters. |
| `anthropic` | bool | True where the source is Anthropic primary material. |
| `nlm_id` | NotebookLM source UUID | Round-trip handle. Optional. |

### 6.5 Person and organisation notes

| Field | Values | Notes |
|---|---|---|
| `name` | free string | Display name. |
| `slug` | kebab-case | Matches folder. |
| `kind` | `person`, `organisation` | Discriminator. |
| `role` | free string | Primary role. |
| `affiliations` | list of strings | Current and past. |
| `key_sources` | list of wikilinks | Sources by or about the entity. |

### 6.6 Concept, architecture, and pattern notes

| Field | Values | Notes |
|---|---|---|
| `name` | free string | Display name. |
| `slug` | kebab-case | Matches filename. |
| `synonyms` | list of strings | Aliases the wiki resolves here. |
| `defined_in` | wikilink | Source that establishes the definition. |
| `related_concepts` | list of wikilinks | Cross-links. |
| `maturity` | `emerging`, `established`, `declining` | For patterns and architectures. |

### 6.7 Auto-generated stamps

Set by tooling. Not edited by hand. `wiki_indexed`, `wiki_hash`, `wiki_role`,
`nlm_last_sync`, `watchlist_channel`.

---

## 7. Tagging Strategy

Two layers. The controlled `topic` layer drives MOCs and Dataview. Every note
carries at least one `topic` value. The open `tags` layer captures folksonomy
that has not earned a controlled slot. A tag that recurs across many notes
graduates to the `topic` vocabulary through a schema update.

---

## 8. Templates

Nine templates in `90_Templates/`, each a frontmatter block plus a body
skeleton:

`concept`, `architecture`, `pattern`, `anti-pattern`, `guide`, `source`,
`person`, `release-note`, `moc`.

Each template carries the required fields from 6.1 and the type-specific fields.
Each body skeleton names the sections the note type expects, for example a
pattern template names Context, Forces, Solution, Trade-offs, When to Use, When
to Avoid, and Related.

---

## 9. MOC Hierarchy

One root and twenty-two topic MOCs, all in `50_MOCs/`.

- `MOC - Home` links the four bands and the twenty-two topic MOCs.
- Foundations band: Foundations, Concepts, Architectures, Agent Patterns.
- Anthropic band: Claude SDK, Claude Code, MCP, Tool Use, Release Notes,
  Boris Cherny.
- Engineering band: Memory, Planning, Prompt Engineering, Multi-Agent,
  Deployment, Observability, Evaluation, Security.
- Practice band: Best Practices, Anti-Patterns, Research Papers, Meta.

Each MOC collects wikilinks and a Dataview query that lists every note carrying
its `topic` value. MOCs collect links, not transcluded content.

---

## 10. Seed Content — 22 Notes

One Home hub plus twenty-one notes across four bands. Each note cites live
primary sources fetched during the build. Anthropic material sets `anthropic:
true`.

The count is one Home hub plus twenty-one band notes, twenty-two in total. The
`MOC - Home` counts among the twenty-three MOCs, not the seed twenty-two.

**Home and navigation (1):** `00_Home/index` hub.

**Foundations (6):** what-is-an-ai-agent; agent-vs-llm; the-agent-loop;
tool-use; memory; planning-and-reasoning.

**Architectures (5):** react; plan-and-execute; reflexion;
supervisor-worker-multi-agent; workflow-vs-autonomous-agent.

**Anthropic core (5):** mcp; claude-agent-sdk; claude-code; prompt-engineering;
one release note in `10_Sources/Release-Notes/`.

**Practice and reference (5):** best-practices-index; anti-patterns-index;
boris-cherny profile stub; glossary skeleton; evaluation.

Each note carries: a one-paragraph summary, key concepts, at least three
outbound wikilinks, a Sources section with live citations, and correct
frontmatter. No note ships isolated.

---

## 11. Cross-Link Strategy

- Every concept links to at least three related concepts.
- Every source links to at least one concept, person, or organisation.
- Every person and organisation profile links to at least one source.
- Every seed note links to its topic MOC, and the MOC links back.
- The glossary links each term to its defining concept note.
- No orphan notes. The build verifies zero orphans among seed notes.

---

## 12. Research Pipeline

The pipeline mirrors `wiki-tokenise` and stays self-contained. It does not
depend on the thinkers-coupled plan scripts.

Evidence: `wiki-tokenise/99_Meta/wiki-tokenise/watchlist.md:35` shows the
channel-table format this design adapts.

### 12.1 Watchlist

`99_Meta/wiki-agents/watchlist.md` holds a channel table. Columns: `channel`,
`name`, `category`, `cadence`, `target_per_run`, `status`. Seed channels:

| channel | name | category |
|---|---|---|
| anthropic-docs | Anthropic Documentation | Anthropic |
| anthropic-engineering | Anthropic Engineering Blog | Anthropic |
| anthropic-news | Anthropic News and Release Notes | Anthropic |
| anthropic-github | anthropics GitHub org | Anthropic |
| claude-code-changelog | Claude Code Changelog | Anthropic |
| arxiv-agents | arXiv cs.AI and cs.MA agent tags | Academia |
| boris-cherny | Boris Cherny talks, posts, and interviews | People |

### 12.2 Monitor

A self-contained monitor design, one per-channel state file under
`99_Meta/wiki-agents/state/<channel>.json`, and a per-channel query file under
`99_Meta/wiki-agents/queries/<channel>.md`. The monitor plans queries against a
channel surface, fetches sources published since `last_run_at`, writes one
source note per accepted candidate, and updates state. It stops at
`target_per_run` or after three dry rounds.

### 12.3 Workflows

Four documented workflows in `99_Meta/wiki-agents/`:

- **Daily research.** Triage `00_Inbox`, run one or two channels, enrich stubs.
- **Weekly maintenance.** Run all active channels, refresh MOCs, check for
  orphans and broken links, update the roadmap.
- **Release-note ingestion.** On an Anthropic release, write a release note from
  the template, link engineering implications, update the Release Notes MOC.
- **NotebookLM ingestion.** Push sources to a NotebookLM notebook, pull briefs
  and audio into `10_Sources/NotebookLM-Exports/`, back-link to source notes.

---

## 13. NotebookLM Bridge

`99_Meta/NotebookLM-bridge.md` documents the round-trip contract: which notes
sync, how `nlm_id` maps a source note to a NotebookLM source, and where exports
land. The bridge treats NotebookLM as the primary research corpus for
authoritative material.

---

## 14. Automation and Integrations

- **Recommended plugins.** Dataview, Tasks, Templater, Obsidian Git. Documented
  in `99_Meta/plugins.md` with the reason for each.
- **Dataview.** Each MOC carries a query listing notes by `topic`. A vault
  dashboard lists stubs, orphans, and recent additions.
- **Tasks.** The weekly-maintenance checklist uses Tasks-format checkboxes so
  the maintenance loop tracks as queryable tasks.
- **Mermaid library.** `80_Attachments/mermaid/` holds reusable diagram sources:
  the agent loop, ReAct, plan-and-execute, supervisor-worker, and a deployment
  pipeline.
- **Claude Code automation.** A short `_CLAUDE.md` at the vault root states the
  vault conventions for future agent sessions.

---

## 15. Canonical Reading Order

The Home hub states a beginner-to-advanced path:

1. what-is-an-ai-agent
2. agent-vs-llm
3. the-agent-loop
4. tool-use
5. memory
6. planning-and-reasoning
7. prompt-engineering
8. react
9. plan-and-execute
10. reflexion
11. mcp
12. claude-agent-sdk
13. claude-code
14. supervisor-worker-multi-agent
15. workflow-vs-autonomous-agent
16. evaluation
17. best-practices-index
18. anti-patterns-index

---

## 16. Roadmap for Continuous Expansion

`99_Meta/roadmap.md` records the growth path:

- Milestone 1: foundation (this pass).
- Milestone 2: Anthropic corpus depth — SDK, Claude Code, MCP guides and code
  examples.
- Milestone 3: full Boris Cherny extraction.
- Milestone 4: release chronology backfill.
- Milestone 5: architecture deep-dives and multi-agent case studies.
- Milestone 6: evaluation and observability tooling guides.

New releases integrate as release notes and source notes. Structure holds.

---

## 17. Success Criteria

### 17.1 Automated verification

- Folder spine exists:
  `test -d 00_Home && test -d 10_Sources && test -d 50_MOCs && test -d 90_Templates && test -d 99_Meta`.
- Schema present: `test -f 99_Meta/schema.md`.
- Nine templates present: `test $(ls 90_Templates/ | wc -l) -ge 9`.
- Twenty-three MOCs present: `test $(ls "50_MOCs/" | grep -c "^MOC - ") -ge 23`.
- Twenty-two seed notes present: count concept, guide, source, and person notes
  outside templates and MOCs equals 22.
- Every seed note has frontmatter: `grep -L "^---" <seed notes>` returns empty.
- Every seed note carries a `topic`: `grep -L "topic" <seed notes>` returns empty.
- No orphan seed notes: a link-check script reports zero seed notes with zero
  inbound and zero outbound wikilinks.
- Watchlist present: `test -f 99_Meta/wiki-agents/watchlist.md`.

### 17.2 Manual verification

- The Home hub opens and the reading order reads in a sensible progression.
- Each MOC renders its Dataview query once Dataview is installed.
- Seed-note citations resolve to live primary sources.
- Anthropic notes carry `anthropic: true` and cite Anthropic material.
- The graph view shows a connected cluster, not scattered nodes.

---

## 18. Phases

The build breaks into four phases. Each verifies on its own. A human confirms
the manual criteria before the next phase starts.

- **Phase 1 — Skeleton.** Folders, schema, templates, plugin and roadmap docs.
  Verify: folder, schema, and template checks in 17.1.
- **Phase 2 — MOCs and navigation.** Twenty-three MOCs, Home hub, reading order,
  Dataview queries. Verify: MOC count, Home renders.
- **Phase 3 — Seed content.** Twenty-two live-sourced notes, cross-linked.
  Verify: seed count, frontmatter, topic, orphan checks; citations resolve.
- **Phase 4 — Pipeline and integrations.** Watchlist, monitor spec, four
  workflows, NotebookLM bridge, Mermaid library. Verify: watchlist present,
  workflows documented.

---

End of design.
