---
type: source
status: draft
created: 2026-08-13
title: "Loop Engineering: The Anthropic Playbook for Designing Systems That Prompt Your Agents"
authors:
- HuaShu
organisation: Orange Books
source_type: paper
venue: 2026 Working Note on Agentic Software Engineering Practice
url: https://huasheng.ai/orange-books
year: 2026
date_published: 2026-06
anthropic: false
topic:
- topic/agent-patterns
- topic/best-practices
tags:
- loop-engineering
- generator-evaluator
- scheduling
- coding-agents
- verification-debt
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
---

# Loop Engineering: The Anthropic Playbook for Designing Systems That Prompt Your Agents

> HuaShu, "Loop Engineering: The Anthropic Playbook for Designing Systems That Prompt Your Agents. A Field Study of Designing Loops That Run Themselves", 2026 Working Note on Agentic Software Engineering Practice, June 2026, https://huasheng.ai/orange-books. Reformats the open guide "Loop Engineering: Stop Asking Me What It Is", Orange Books, v260615.

## Summary

The title claims an Anthropic playbook. The extract contradicts the title. The
copyright line reads "©2026 HuaShu" and describes the document as an
independent reformatting of HuaShu's own Orange Book guide. The acknowledgment
credits the framework to Addy Osmani, an engineer on the Google Chrome team.
Anthropic staff appear as cited sources, not as authors: Boris Cherny on
writing loops, and Prithvi Rajasekaran on the generator and evaluator split.
No Anthropic authorship and no Anthropic endorsement appear anywhere in the
extract. The `anthropic` field stays false. On substance, the note defines
loop engineering as a fourth layer above prompt, context, and harness
engineering. The practitioner stops prompting the agent and builds the system
that prompts it. One turn of a loop runs five moves, realised by six parts.
Generation becomes cheap; judgement stays scarce.

## Key Concepts

- Loop engineering replaces the person who prompts the agent with a system that prompts it.
- The four-layer stack runs prompt, context, harness, then loop. Each layer minds a larger unit.
- Three verbs separate a loop from a harness: it runs on a timer, it spawns helpers, and it feeds itself.
- One turn holds five moves: discovery, handoff, verification, persistence, and scheduling.
- Six parts realise the moves: automations, worktrees, skills, connectors, sub-agents, and memory.
- An agent that grades its own output praises it. A separate evaluator is the fix.
- The cost of a mistake scales with the number of turns it survives before discovery.
- Reliability comes from the quality of the constraints, not the size of the model.

## Terminology

- Loop - a system that discovers, does, verifies, persists, and reschedules work with no human in the inner cycle.
- Harness - the kit arming a single agent run: tools, allowed actions, recovery, and the definition of done.
- Move - one of the five steps in a single turn of a loop.
- Part - one of the six components that realise the moves.
- Generator - the agent that writes.
- Evaluator - a separate agent that judges, defaults to doubt, and acts to verify.
- Worktree - a git mechanism giving each parallel agent its own working directory.
- Skill - project knowledge made permanent in a `SKILL.md` file.
- Connector - an MCP interface linking the loop to external systems.
- Memory - persistent state on disk, surviving any single conversation.
- Intent debt - the recurring cost of re-explaining a project, paid off by a skill.
- Verification debt - unverified output accumulating in the gap between "runs" and "right".

## Architecture and Implementation

The note stacks four layers. Prompt minds the words for one exchange. Context
minds the window. Harness arms one run. Loop makes the run repeat. Each layer
fails with a different blast radius. A prompt error surfaces at once. A loop
error is written to the state file, read back as fact, and built upon for
days.

One turn runs five moves. Discovery finds the work and sets the ceiling on
loop quality. Handoff cuts each task into an isolated git worktree. Verification
swaps in a second agent to say no. Persistence writes state outside the
conversation. Scheduling turns one run into a loop.

Section V separates the generator from the evaluator. The generator's context
holds the reasons the code was written, so it reviews its own chain of
self-persuasion. The note borrows the split from generative adversarial
networks. The evaluator takes a different model, different instructions, and a
default stance of doubt. It acts through Playwright MCP: it opens the page,
clicks, screenshots, and inspects the DOM. Claude Code's `/goal` runs turns
until a stop condition holds, and a fresh small model judges the condition.
The note names this the maker-checker principle from banking.

Stripe's Minions pipeline shows the enterprise shape. A Slack mention or an
emoji reaction triggers it. A deterministic orchestrator assembles context
first: it scans links, pulls Jira, and locates code through Sourcegraph and
MCP. The model writes code. A hard-coded gate runs the linter, and the agent
cannot skip it. A hard-coded step commits. Humans review the output. Minions
forks the open-source Goose framework and runs on Devbox on EC2, on a cattle
not pets basis.

Table IV compares schedulers. Cloud runs with the machine off and takes a
one-hour minimum interval. Desktop and `/loop` need the machine on, reach a
one-minute interval, and see local files. Table V maps the same six
capabilities across Claude Code and Codex.

## Code Examples

The note carries five reusable artefacts. Section V gives an adversarial
reviewer agent for `.claude/agents/reviewer.md`, which assumes the code is
broken until proven otherwise and returns PASS or REJECT with reasons. It
gives a `/goal` stop condition: all tests in `test/auth` pass and the lint step
is clean. Section XII gives `/loop` invocations, a `morning-triage` skill under
`.claude/skills/`, and a `./state/triage.md` table with one row per finding.
Section XII.A gives a complete first loop as a GitHub Actions cron workflow,
annotated with six numbered comments matching the checklist. Appendix A gives
a fuller triage skill whose six headings map to the five moves plus a "Stop"
section.

## Best Practices

- Trigger a named skill from the automation, never a wall of text pasted into a cron job.
- Tune an independent sceptic instead of asking the author to doubt itself.
- Make the evaluator act rather than read. Judge behaviour, not intent.
- Hand the stop decision to a fresh model, not the model doing the work.
- Keep deterministic work out of the probabilistic model. Hard-code every rule that admits one.
- Write findings and status to a file on disk. The agent forgets; the repo does not.
- Set a per-run budget, a daily budget, and a maximum retry count before the first unattended run.
- Read a sampled change each day and explain what it did and why.
- Keep one checkpoint where the loop pauses for a human. Open pull requests; never auto-merge.
- Add parallelism last, after the evaluator has caught real mistakes.

## Warnings and Anti-Patterns

- The nodding loop skips verification. The writer grades its own homework and the loop never says no.
- The amnesiac loop skips persistence. State dies with the context window and each morning starts over.
- The manual loop skips scheduling. It runs on the demo day, then never again.
- The blind loop skips discovery. A human still picks the work, which is the expensive part.
- The tangled loop skips handoff. Parallel agents edit one directory and the merge collapses.
- Verification debt accrues in the gap between code that runs and code that is right.
- Comprehension rot widens the gap between the codebase and the map in the builder's head.
- Cognitive surrender arrives when the builder stops holding an opinion.
- Token blowout follows retries and spawned helpers. One idle bug burns a night's quota.
- The four costs reinforce each other and come due at once.
- Treat circulated figures such as "90% of Claude Code is written by itself" as secondhand.

## Related Concepts

- [[the-agent-loop]]
- [[workflow-vs-autonomous-agent]]
- [[supervisor-worker-multi-agent]]
- [[evaluation]]
- [[memory]]
- [[mcp]]
- [[claude-code]]
- [[anti-patterns-index]]
- [[best-practices-index]]

## Future Work

The note flags the naming lag as the place to watch. Practice arrives first and
the name follows, so the next term will come from a capability that turns cheap
enough to make a new composition routine. It records Codex cloud scheduling as
planned rather than shipped. It states that no single scheduler covers every
case, and that a mature loop runs local and cloud together. It closes the
technical thread and hands the rest to the terminal.

## References

- HuaShu, "Loop Engineering: Stop Asking Me What It Is", Orange Books, v260615, June 2026 - https://huasheng.ai/orange-books
- A. Osmani, "Loop Engineering", personal blog and Substack, June 2026
- P. Steinberger, post on designing loops that prompt coding agents, June 2026
- B. Cherny, public remarks on writing loops that prompt Claude, Anthropic, June 2026
- P. Rajasekaran, "Building long-running agentic applications: the generator/evaluator pattern", Anthropic engineering blog, 2026
- S. Kaliski, "Stripe's Minions: 1,300 PRs a week", How I AI podcast, 2026
- "Model Context Protocol (MCP) specification", open standard, 2025 to 2026
- "Goose: an open-source agent framework", project documentation, 2025 to 2026
- "Claude Code documentation: /loop, /goal, worktrees, skills, automations", Anthropic, 2026

## See also

- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]] - the vault's Anthropic primary source on agents and workflows
- [[10_Sources/Docs/claude-code-overview|Claude Code Overview]] - the toolchain this note builds loops on
- [[10_Sources/Books/agentic-design-patterns-gulli-2025|Agentic Design Patterns]] - pattern catalogue covering reflection and multi-agent splits
- [[agent-patterns-index]] - consolidated pattern reference
