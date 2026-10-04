---
type: source
status: draft
created: 2026-07-15
title: Claude Code dynamic workflows
authors: []
organisation: Anthropic
source_type: docs
venue: code.claude.com
url: https://code.claude.com/docs/en/workflows
year: 2026
date_published: 
anthropic: true
topic:
- topic/concepts
tags: []
nlm_id: 
nlm_skip: false
watchlist_channel: 
af_targets:
- af:DELEG-01
- af:RSCH-01/claude-code
- af:RSCH-04/Q05
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 7d34968f6148fd8b04bb4ae2d8b26f303691133b369b90c590223cd9dd76a4bb
---

# Claude Code dynamic workflows

> Anthropic, "Dynamic workflows", code.claude.com, 2026. https://code.claude.com/docs/en/workflows

## Summary

A dynamic workflow is a JavaScript script that orchestrates subagents at scale. Claude writes the script for the task described. A runtime executes it in the background while the session stays responsive. Reach for a workflow when a task needs more agents than one conversation can coordinate, or when the orchestration should become a script to read and rerun.

## Key Concepts

- Who-holds-the-plan differs across four approaches. A subagent is a worker Claude spawns, and Claude decides turn by turn. A skill is instructions Claude follows, and Claude decides while following the prompt. An agent team is a lead supervising peer sessions, and the lead decides turn by turn. A workflow is a script the runtime executes, and the script decides what runs next.
- "A workflow moves the plan into code." Claude's context holds only the final answer, while intermediate results live in script variables.
- Scale spans dozens to hundreds of agents per run. A run allows up to 16 concurrent agents and 1,000 agents in total.
- Three triggers start a workflow: the keyword `ultracode` in a prompt, a natural-language opt-in such as "use a workflow", and `/effort ultracode` for every substantive task in the session.
- Save a workflow for reuse. Saved workflows become `/commands` from `.claude/workflows/` or `~/.claude/workflows/`, and the project version wins on a name clash.

## Terminology

- Dynamic workflow — a JavaScript script Claude writes that a runtime executes in the background.
- ultracode — the keyword that tells Claude to plan a workflow for a task.
- acceptEdits mode — the mode a workflow's subagents always run in, so file edits are auto-approved.

## Best Practices

- Run adversarial cross-review of findings before reporting.
- Run each sign-off stage as its own workflow, because a run cannot pause for user input between stages.
- Start with the bundled `/deep-research` workflow.

## Warnings and Anti-Patterns

- A workflow accepts no mid-run user input; only agent permission prompts pause a run. Interactive intake and approval gates cannot run inside a workflow.
- A workflow is a run-time execution substrate, not a recommendation layer.
- A run costs far more tokens than conversation. A "Large workflow" warning fires past 25 agents or 1.5M projected tokens.

## Related Concepts

- [[agent-patterns-index]]
- [[workflow-vs-autonomous-agent]]

## References

- https://code.claude.com/docs/en/workflows
