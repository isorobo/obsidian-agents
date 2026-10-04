---
title: Wiki refresh 2026-10-04
type: report
date: 2026-10-04
tags: [metadata, wiki-refresh]
auto_generated: true
---

# Wiki refresh 2026-10-04

First `/wiki` stamping pass on this vault, run interactively with the operator's approval. Frontmatter only.

## Scan

| Measure | Count |
|---|---|
| Notes scanned | 132 |
| Fresh before apply | 132 |
| Quarantined | 0 |
| Orphans | 0 |
| Cap violations | 0 |
| Vocabulary values | 27 (schema.md section 2.3) |
| Off-vocabulary topics in use | 0 |

## Newly tagged

One topic added. `20_People/andrej-karpathy/profile.md` carried only `topic/karpathy`, a band topic that needs a general companion. Added `topic/best-practices` (confidence about 0.72: the profile's Key Positions cover review, oversight and eval practice). Listed for attention. Apply is append-only, so removal is a manual edit.

## Re-stamp only

128 notes received `wiki_hash`, `wiki_indexed` and no topic change. All their existing topics were already on the vocabulary. This includes four meta notes that needed a stamp only (`00_Home/index.md`, `99_Meta/agens-log.md` and the two `99_Meta/design/` notes).

Apply result: 129 applied, 0 unchanged, 0 failed. Plan-check passed with 0 errors. The dry run touched only `wiki_indexed`, `wiki_hash` and the one `topic` line.

## Held (3)

| Path | Reason |
|---|---|
| `10_Sources/Talks/source-slug.md` | 0-byte file. No frontmatter and no body to classify. Probably a template leftover. |
| `99_Meta/schema.md` | Protected path. The wiki-agents contract bars stamping it. |
| `99_Meta/agent-factory/af-targets.md` | Protected path. Same reason. |

These three stay fresh by design. `verify` reports `ok: true` with no unexpected paths.

## Pending Topic candidates

None. No off-vocabulary values and no staged candidates.

Band topic check: every band-topic note (`topic/karpathy`, `topic/agent-skills`, `topic/retrieval`, `topic/domain-applications`, `topic/learning`) has a general partner after this pass. No note exceeds 3 topics.

## Schema issues

None found. `rule_warnings` had two entries: the empty stub (held) and the Karpathy companion (fixed above).

## MOC candidates

Suggest mode. Nothing written to `50_MOCs/`. 122 notes considered, 28 already linked from a MOC, 147 candidate placements across 22 MOCs (a note with two topics appears under two MOCs), 0 unmapped. The full list is in `wiki-moc-candidates-2026-10-04.json`, grouped by MOC: Agent Patterns, Anti-Patterns, Architectures, Best Practices, Boris Cherny, Claude Code, Claude SDK, Concepts, Deployment, Domain Applications, Evaluation, Foundations, Karpathy, MCP, Memory, Multi-Agent Systems, Planning, Prompt Engineering, Release Notes, Research Papers, Security, Tool Use. Most candidates are expected: the MOCs are Dataview queries over `topic`, so notes surface without a wikilink.

## Part A: linking pass

One monitor note was created in the window: `10_Sources/Blog/anthropic-how-we-contain-claude.md`. Its four concept targets (`claude-code`, `tool-use`, `mcp`, `best-practices-index`) already list it under `## Sources`. No edits made. No profile links, no new release notes, no missing concepts.

## Housekeeping observations

- `10_Sources/Talks/source-slug.md` is empty. Delete or fill it (user decision).
- `anthropic-how-we-contain-claude.md` has `status: draft`. Its Summary says "Page access was via the primary page", which is fine.
- Nearly every source note carries `watchlist_channel`, so the Part A fallback window is set by `created` date, not by that key.

## Working tree

157 dirty paths from `git status --porcelain`, covering this pass plus earlier uncommitted engine-rebuild edits. Nothing committed. Suggested message: `Stamp wiki_hash and wiki_indexed on 129 notes (first /wiki apply)`.

## Pending your decision

- Confirm or revert `topic/best-practices` on the Karpathy profile.
- Delete or fill `10_Sources/Talks/source-slug.md`.
- Stamping `99_Meta/schema.md` and `99_Meta/agent-factory/af-targets.md` is barred by the contract. They will show as fresh on every run unless the contract or `never_write` changes.
- Standing: promote the `anthropic-news` pilot once it has a clean cycle; auto-commit on or off; watchlist surface and cadence edits recommended by monitors (none this run).

## Next steps

1. Commit the stamping pass.
2. Run `/wiki-agents af-tag --all` then `digest`.
3. Next `/wiki-agents wiki-refresh` will re-stamp only modified notes.

## Second pass (headless wiki-refresh)

Run later the same day with `--headless`. Plan: `apply-plan-2026-10-04-2.json`. MOC candidates file `wiki-moc-candidates-2026-10-04.json` was overwritten by this pass.

| Measure | Count |
|---|---|
| Notes scanned | 176 |
| Fresh before apply | 47 (44 monitor notes created since the first pass, 3 held) |
| Stamped (existing topics confirmed, no topic change) | 44 |
| Held | 3 (`10_Sources/Talks/source-slug.md` still a 0-byte stub; `99_Meta/schema.md` and `99_Meta/agent-factory/af-targets.md` never_write) |
| Off-vocabulary topics | 0 |
| Pending Topic candidates | 0 |
| Band-topic violations | 0 |
| Notes above 3 topics | 0 |

Apply result: 44 applied, 0 unchanged, 0 failed. Dry run touched only `wiki_indexed` and `wiki_hash`. Verify: `ok: true`, no unexpected paths.

### MOC candidates

Suggest mode. Nothing written to `50_MOCs/`. 44 notes considered, 0 already linked from a MOC, 102 candidate placements across 20 MOCs, 0 unmapped. Every topic has a MOC.

### Part A: linking pass

All edits append-only. Window: monitor notes created in the last 14 days (none of the 44 was linked from any concept or profile before this pass).

- Appended source bullets to the `## Sources` section of 16 concept notes: `the-agent-loop`, `tool-use`, `memory`, `claude-code`, `claude-agent-sdk`, `mcp`, `evaluation`, `supervisor-worker-multi-agent`, `workflow-vs-autonomous-agent`, `prompt-engineering`, `plan-and-execute`, `react`, `reflexion`, `planning-and-reasoning`, `what-is-an-ai-agent`, `best-practices-index`. About 130 bullets in all, one per source note and linked concept.
- Concept bodies changed, so all 16 were re-stamped with `wiki_tool.py stamp` (hash and indexed only).
- `20_People/ai-builder-club/profile.md`: five entries added to `key_sources`.
- `20_People/boris-cherny/profile.md`: two entries added to `key_sources`.
- Concepts linked by the new notes with no `## Sources` heading: none missing a heading. Concept notes linked but not edited because the new notes did not link them: none.

Release-note comparison (Part A step 3): not performed in this headless run. See Pending your decision.

### Housekeeping observations

- `10_Sources/Talks/source-slug.md` is still a 0-byte file (carried from the first pass).
- A multi-line `rg` command was denied by the headless allow list. The plan was built from the scan JSON read directly instead (flag `permission-denied:rg-multiline`).
- Working tree: 105 dirty paths. Nothing committed. Suggested message: `Stamp wiki_hash on 44 monitor notes and backlink them into 16 concepts and 2 profiles`.

### Pending your decision

- Release notes 2.1.285 to 2.1.289, Opus 5.5, Sonnet 5.5 and Fable 5.1 have not been compared against the Summary, Detail and Trade-offs text of `claude-code`, `claude-agent-sdk` and `mcp`. Run that comparison interactively so each sentence change can be proposed and approved.
- Delete or fill `10_Sources/Talks/source-slug.md`.
- Standing: promote the `anthropic-news` pilot once it has a clean cycle; auto-commit on or off.
