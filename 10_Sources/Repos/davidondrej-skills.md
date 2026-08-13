---
type: source
status: draft
created: 2026-07-11
title: "davidondrej/skills"
authors:
- David Ondrej
organisation: davidondrej (GitHub)
source_type: repo
venue: GitHub
url: https://github.com/davidondrej/skills
year: 2026
date_published:
anthropic: false
topic:
- topic/best-practices
- topic/agent-skills
tags:
- agent-skills
- claude-code
nlm_id:
nlm_skip: false
watchlist_channel:
---

# davidondrej/skills

> David Ondrej, "skills", GitHub repository, https://github.com/davidondrej/skills. MIT licence, copyright David Ondrej 2026.

## Summary

A collection of 27 reusable Agent Skills for AI coding, research, and workflow agents, organised into five category folders rather than a flat list. The README's own framing: each skill "packages a focused workflow into instructions that an agent can load when the task calls for it," aimed at "improving codebases, preparing content, researching ideas, reviewing presentations, working with transcripts, and other repeatable workflows." The repository follows the same folder-plus-`SKILL.md` structure already documented in this vault's [[10_Sources/Blog/agent-skills-best-practices|Anthropic Claude Code Skills note]].

## Key Concepts

- Five category folders, twenty-seven skills total:
  - **Agent Orchestration** (7): `agent-self-scheduling`, `cmux`, `codex-subagent`, `fable-safe-prompt`, `goal-loop`, `handoff`, `run-deep-swe`.
  - **Ops and Setup** (6): `anti-sleep`, `create-readonly-db-role`, `cyber-audit`, `google-safe-browsing`, `pi-custom-model`, `setup-help`.
  - **Research and Web** (7): `browser-harness`, `deep-research`, `deepapi`, `online-shopping`, `pi-web-search`, `research-prompt`, `youtube-transcript`.
  - **Skill Authoring** (4): `distribute-skill-to-all-agents`, `effective-agent-skills`, `folder-specific-claude-and-agents-md`, `push-skill-to-github`.
  - **Thinking and Docs** (6, one with sub-format guides): `brain-to-docs`, `level-up`, `prompt-me`, `read-all-adrs`, `short`, `teach` (the `teach` skill bundles additional format guides for glossaries, learning records, missions, and resources).
- Each skill lives in its own folder with a `SKILL.md` file, matching the folder-not-file format the Anthropic playbook describes.
- The Skill Authoring category is itself notable: `distribute-skill-to-all-agents`, `push-skill-to-github`, and `folder-specific-claude-and-agents-md` are skills for building and publishing more skills — a self-hosting pattern on top of the format.

## Terminology

No terms beyond the standard Agent Skill vocabulary already defined in [[10_Sources/Blog/agent-skills-best-practices|the Anthropic Skills note]] (Skill, progressive disclosure, trigger signal).

## Architecture and Implementation

Confirmed via the repository's GitHub API file tree: top-level `README.md`, `LICENSE` (MIT), and `.gitignore`, with a `skills/` directory holding the five category subfolders listed above, each containing one folder per skill with its own `SKILL.md`. No explicit install command (such as an `npx skills add` invocation) appears in the README, unlike this vault's other two Skills-library sources ([[10_Sources/Blog/google-skills-official-library|google/skills]], [[10_Sources/Blog/last30days-real-time-research-skill|last30days-skill]]). The standard convention documented elsewhere in this vault — cloning or copying a skill folder into a `.claude/skills/` directory — likely applies, but this repository does not state that explicitly, so it is an inference, not a confirmed fact.

## Code Examples

None found in the fetched content; individual `SKILL.md` files were not read in this pass.

## Best Practices

Inherits the general Agent Skills best practices already captured from Anthropic's playbook: fit a skill to one workflow, write descriptions as trigger phrases, keep detail in `references/` rather than a single bloated `SKILL.md`. The repository's own Skill Authoring category (`effective-agent-skills`, `folder-specific-claude-and-agents-md`) suggests it carries its own opinions on this beyond the Anthropic baseline, not yet read in full here.

## Warnings and Anti-Patterns

None stated in the content retrieved so far.

## Related Concepts

- [[best-practices-index]]
- [[claude-code]]
- [[10_Sources/Blog/agent-skills-best-practices|Anthropic's 300+ Claude Code Skills: Lessons Learned]]
- [[10_Sources/Blog/google-skills-official-library|google/skills: Google's Official Agent Skills Library]]
- [[10_Sources/Blog/last30days-real-time-research-skill|last30days-skill: Real-Time Research for AI Agents]]

## Future Work

The individual `SKILL.md` files (27 of them) have not been read; a deeper pass could extract per-skill detail the way the course lessons were extracted, particularly for `goal-loop`, `handoff`, and `run-deep-swe` under Agent Orchestration, which sound closely related to this vault's existing multi-agent and supervisor/worker notes.

## References

- davidondrej/skills (GitHub repository) — https://github.com/davidondrej/skills
- LICENSE (MIT, copyright David Ondrej 2026) — https://raw.githubusercontent.com/davidondrej/skills/main/LICENSE
