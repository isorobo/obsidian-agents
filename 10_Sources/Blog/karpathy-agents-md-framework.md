---
type: source
status: draft
created: 2026-07-11
title: "Karpathy's agents.md: What It Is and Why It Matters"
authors:
- Jason Zhou
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 1.10 (speculative commentary on Andrej Karpathy's public statements; Karpathy had not published an agents.md at time of writing)
url: https://www.aibuilderclub.com/blog/karpathy-agents-md-framework
year: 2026
date_published: 2026-06-09
anthropic: false
topic:
- topic/best-practices
- topic/karpathy
tags:
- karpathy
- agents-md
- permission-boundaries
- course
nlm_id:
nlm_skip: false
watchlist_channel:
---

# Karpathy's agents.md: What It Is and Why It Matters

> Jason Zhou, "Karpathy's agents.md: What It Is and Why It Matters", AI Builder Club, Build AI Agents Course, 9 June 2026, https://www.aibuilderclub.com/blog/karpathy-agents-md-framework. The article states plainly that Karpathy had not published an agents.md at time of writing; this is speculative analysis built from his public statements, not his own document.

## Summary

Karpathy's existing `claude.md` addresses AI-assisted coding under human interaction (think before coding, simplicity first, surgical changes, goal-driven execution). The lesson argues a hypothetical `agents.md` would need to differ fundamentally, because autonomous systems fail at different points, carry different trust boundaries, and need different prompting than an assisted-coding workflow. It synthesises four recurring themes from Karpathy's public statements into four proposed rules, while an existing formal `AGENTS.md` standard, under Linux Foundation stewardship and supported across Codex, Cursor, Windsurf, Copilot, Aider, Devin, Amp, opencode, and RooCode, already exists independently of Karpathy.

## Key Concepts

- Agent failures concentrate at handoffs between tools, ambiguous instructions, and unexpected input formats — boundary failures, not core capability gaps.
- Autonomy should scale with an action's reversibility, not with task complexity: low-stakes actions (reading, testing) can run fully automated; high-stakes actions (production deployment, sending email) need a human checkpoint.
- Memory — long-context maintenance, tracking attempted solutions, updating an internal model — remains, in the lesson's framing, the least-solved piece of agent infrastructure.
- Poor tool definitions and overlapping tool capabilities are named as the dominant real-world failure surface.

## Terminology

- agents.md — a cross-tool standard file for AI agent behavioural guidelines and project context, distinct from the human-interaction-focused `claude.md`.
- Permission boundary — an explicit statement of what an agent may read, write, and must never touch.
- Checkpoint — a mandatory human-approval gate placed before a high-stakes or irreversible agent action.

## Architecture and Implementation

The four proposed rules: define permission boundaries explicitly, with READ, WRITE, NEVER, and HUMAN_CHECKPOINT categories stated before any code is written — "be concrete before you're clever"; make tool actions reversible or fully auditable, logging inputs, outputs, and reasoning for every call, with irreversible actions gated behind human approval; fail loudly and stop on an out-of-scope situation rather than improvising past it, since a silent continuing failure is more dangerous than a loud stop; and treat a persistent Markdown memory file, read at session start and written at session end, as the source of truth for learned patterns and failed attempts, not the model's ephemeral context.

## Code Examples

The lesson references an example permission-boundary structure (READ / WRITE / NEVER / HUMAN_CHECKPOINT categories) and points to the FerroxLabs/agents-md repository as a third-party attempt to synthesise Karpathy's principles into one shareable file, without reproducing runnable code.

## Best Practices

- Write permission boundaries before coding begins; keep the document to one page and have a peer review it.
- Make every significant agent action auditable through comprehensive logging.
- Place human checkpoints at task start, at decision points, and before any irreversible action.
- Maintain a structured memory file outside the model's context window as the durable record.

## Warnings and Anti-Patterns

- Treating agent failure as a core-capability problem misdiagnoses boundary and handoff failures as something a bigger model would fix.
- Scaling oversight to task complexity rather than to action reversibility misallocates review effort.
- Relying on the model's context window as memory, rather than a persistent file, loses learned patterns and failed attempts at session end.
- Overlapping or poorly defined tools compound failure surface as tool count grows.

## Related Concepts

- [[tool-use]]
- [[best-practices-index]]
- [[claude-code]]
- [[20_People/andrej-karpathy/profile|Andrej Karpathy]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The article itself flags the gap: production builders have converged on these principles independently, but guidance remains scattered across repos and private channels rather than one authoritative document from Karpathy himself.

## References

- Karpathy's agents.md: What It Is and Why It Matters — https://www.aibuilderclub.com/blog/karpathy-agents-md-framework
