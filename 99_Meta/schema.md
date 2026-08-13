---
type: meta
title: Vault Schema and Controlled Vocabulary
status: permanent
created: 2026-07-10
topic:
- topic/meta
wiki_role: meta
---

# Vault Schema and Controlled Vocabulary

This file defines the controlled frontmatter vocabulary for **wiki-agents**.
Every note conforms to these fields. A new controlled value requires an update
here before use. The schema adapts the sibling `wiki-tokenise` pattern for the
AI-agents domain, with the Anthropic ecosystem as the primary lens.

---

## 1. Folder Purpose

| Folder | Purpose |
|---|---|
| `00_Home/` | Vault entry hub and canonical reading order. |
| `00_Inbox/` | Unprocessed captures awaiting triage. |
| `10_Sources/` | One note per primary source, grouped by source-type subfolder. |
| `10_Sources/PDFs/` | Raw binary downloads. Excluded from version control. |
| `10_Sources/NotebookLM-Exports/` | NotebookLM audio, brief, and slide artefacts. |
| `20_People/<slug>/` | One folder per person or organisation. Holds `profile.md`. |
| `30_Concepts/` | Atomic concept, architecture, pattern, and anti-pattern notes. |
| `40_Guides/` | Implementation guides, engineering guides, tutorials, code examples. |
| `50_MOCs/` | Maps of Content. One Home MOC and twenty-two topic MOCs. |
| `60_Drafts/` | Work-in-progress essays and deep-research outputs. |
| `70_Research/` | Active research threads. One folder per thread. |
| `80_Attachments/` | Images, diagrams, Mermaid source. |
| `90_Templates/` | Templater-compatible templates. |
| `99_Meta/` | Schema, design docs, watchlist, pipeline state, integration docs. |
| `99_Meta/learning/` | Operator learning state: concept ledger, failure log, derived principles. |

---

## 2. Frontmatter Fields

### 2.1 Required on every note

| Field | Enum values | Notes |
|---|---|---|
| `type` | see 2.2 | Governs which template applied. |
| `status` | `inbox`, `stub`, `draft`, `review`, `permanent`, `archived` | Lifecycle state. |
| `created` | ISO date (`YYYY-MM-DD`) | Creation date. |
| `topic` | list from 2.3 | Controlled topic vocabulary. At least one value. |
| `tags` | list of free strings | Open folksonomy; not controlled. |

### 2.2 `type` enum

`concept`, `architecture`, `pattern`, `anti-pattern`, `guide`, `source`,
`person`, `organisation`, `release`, `moc`, `draft`, `glossary`, `meta`,
`project`, `failure`, `principle`, `ledger`.

`project`, `failure`, `principle`, and `ledger` (added 2026-08-13) serve the
learning system in `99_Meta/learning/`. A `project` note records one build:
its learning objective, its design decisions, and what it taught. A `failure`
note records one failure, its class, and the design weakness that allowed it.
A `principle` note states one rule Simon derived from a project or a failure,
and cites the source of the derivation. A `ledger` note holds learner state
and carries no body prose beyond its table. Each of these types takes
`topic/learning` plus at least one general topic, matching the convention
stated for `topic/domain-applications`.

### 2.3 `topic` controlled vocabulary (27)

`topic/foundations`, `topic/concepts`, `topic/architectures`,
`topic/claude-sdk`, `topic/claude-code`, `topic/mcp`, `topic/tool-use`,
`topic/memory`, `topic/planning`, `topic/prompt-engineering`,
`topic/agent-patterns`, `topic/multi-agent`, `topic/deployment`,
`topic/observability`, `topic/evaluation`, `topic/security`,
`topic/best-practices`, `topic/anti-patterns`, `topic/release-notes`,
`topic/boris-cherny`, `topic/karpathy`, `topic/agent-skills`,
`topic/retrieval`, `topic/research-papers`, `topic/domain-applications`,
`topic/meta`, `topic/learning`.

`topic/learning` (added 2026-08-13) covers the operator's own learning state
and the artefacts that record it: the concept ledger, the failure log, project
retrospectives, and derived principles. It describes what Simon has learned
and how, not what an agent retains, which stays with `topic/memory`. It is
distinct from `topic/foundations`, which describes the subject matter itself.
A note in this topic carries a second, general topic alongside it, matching
the `topic/karpathy` and `topic/agent-skills` convention.

`topic/retrieval` (added 2026-08-12) covers the retrieval substrate an agent
depends on: vector and hybrid search, knowledge graph construction, graph
databases, and GraphRAG. It is distinct from `topic/memory`, which covers what
an agent retains across turns and sessions. Retrieval is the lookup mechanism;
memory is the retained state. A source may carry both. The vocabulary
graduated from a five-source cluster (Neo4j's graph database and knowledge
graph guides, Manning's `Essential GraphRAG`, Elastic's semantic search
whitepaper, and Graphwise's `The Semantic Advantage`) under the rule stated
for `topic/domain-applications`. Each source in this topic carries a second,
general topic alongside it, matching the `topic/karpathy` and
`topic/agent-skills` convention.

`topic/karpathy` (added 2026-07-11) covers Andrej Karpathy's public talks,
posts, and third-party commentary on them, mirroring the `topic/boris-cherny`
pattern for a second named individual. A source in this topic carries a
second, general topic alongside it (for example `topic/best-practices` or
`topic/memory`) so it also surfaces under the general reading path, per the
same rule stated for `topic/domain-applications` below.

`topic/agent-skills` (added 2026-07-11) covers the Agent Skills pattern
itself — what a Skill is, how it is authored, packaged, distributed, and
installed — as distinct from any one skill's subject matter. Graduated from
a four-source cluster (Anthropic's Claude Code Skills playbook, `google/
skills`, `last30days-skill`, `davidondrej/skills`) via the same rule stated
for `topic/domain-applications`: a tag recurring across many notes earns a
controlled slot. Each source in this topic carries a second, general topic
alongside it, matching the `topic/karpathy` and `topic/domain-applications`
convention.

`topic/domain-applications` (added 2026-07-10) covers agent and NLP research
scoped to one professional domain rather than general agent engineering —
for example agentic and NLP systems applied to law. The vocabulary graduated
directly from a five-plus-paper cluster rather than through the tag layer,
per section 4. Papers in this topic carry a second, general topic (most often
`topic/research-papers`) so they also surface under the general reading path.

### 2.4 Source notes

| Field | Enum or format | Notes |
|---|---|---|
| `title` | free string | Work title. |
| `authors` | list of strings | Author names. |
| `organisation` | free string | Issuing body, for example `Anthropic`. |
| `source_type` | `docs`, `blog`, `paper`, `talk`, `repo`, `changelog`, `release-note`, `interview`, `sdk-reference`, `book`, `tutorial` | Required. |
| `venue` | free string | Conference, journal, site, podcast. Optional. |
| `url` | URL | Canonical link. `TBD` permitted at stub stage. |
| `year` | integer | Publication year. |
| `date_published` | ISO date | Where day-granularity matters. |
| `anthropic` | bool | True where the source is Anthropic primary material. Default false. |
| `nlm_id` | NotebookLM source UUID | Round-trip handle. Optional. |
| `nlm_skip` | bool | If true, excluded from NotebookLM exports. Default false. |

### 2.5 Person and organisation notes

The same folder layout (`20_People/<slug>/`) holds both. The `kind` field
discriminates.

| Field | Enum or format | Notes |
|---|---|---|
| `name` | free string | Display name. |
| `slug` | kebab-case | Matches folder name. |
| `kind` | `person`, `organisation` | Required. |
| `role` | free string | Primary role. |
| `affiliations` | list of strings | Current and past. |
| `key_sources` | list of wikilinks | Sources by, from, or about this entity. |

### 2.6 Concept, architecture, pattern, and anti-pattern notes

| Field | Enum or format | Notes |
|---|---|---|
| `name` | free string | Display name. |
| `slug` | kebab-case | Matches filename. |
| `synonyms` | list of strings | Aliases the wiki resolves here. |
| `defined_in` | wikilink | Source that establishes the canonical definition. |
| `related_concepts` | list of wikilinks | Cross-links. |
| `maturity` | `emerging`, `established`, `declining` | For patterns and architectures. Optional. |

### 2.7 Auto-generated stamps

Set by tooling. Not edited by hand.

| Field | Notes |
|---|---|
| `wiki_indexed` | ISO timestamp of last `/wiki apply` pass. |
| `wiki_hash` | SHA-256 of the normalised note body. Drives idempotent re-runs. |
| `wiki_role` | `wiki`, `meta`, `index`, `moc`, `source`, `person`, `organisation`, `concept`. |
| `nlm_last_sync` | ISO timestamp of last NotebookLM round-trip. |
| `watchlist_channel` | Slug of the watchlist channel that surfaced this source. |

### 2.8 Agent-authorship marker

Set by an agent on any note it writes. Absent on human-authored notes.

| Field | Enum values | Notes |
|---|---|---|
| `authored_by` | `agens` | Present only on agent-written notes; its presence alone marks a note as agent-authored. Absent on a note written by hand. |

---

## 3. Linking Conventions

- People and organisations: `[[20_People/<slug>/profile|Display Name]]`.
- Sources: `[[10_Sources/<Source-Type>/<slug>|Short Title]]`.
- Concepts: `[[<concept-slug>]]`.
- MOCs: `[[MOC - <Name>]]`.
- Every concept links to at least three related concepts.
- Every source links to at least one concept, person, or organisation.
- Every person and organisation profile links to at least one source.
- Every note links to its topic MOC, and the MOC links back.
- MOCs collect wikilinks, not transcluded content.
- No orphan notes.

---

## 4. Tagging Strategy

Two layers. The controlled `topic` layer drives MOCs and Dataview. Every note
carries at least one `topic` value. The open `tags` layer captures folksonomy
that has not earned a controlled slot. A tag that recurs across many notes
graduates to the `topic` vocabulary through an update to section 2.3.

---

## 5. Pilot Channel

The pilot for the watchlist-driven refresh is **anthropic-news**. Its output is
central and high-signal, so errors surface quickly. Once stable, the watchlist
promotes `anthropic-engineering` and `anthropic-docs`, then the remainder.

End of schema.
