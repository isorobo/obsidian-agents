---
type: source
status: draft
created: 2026-10-04
title: "An update on recent Claude Code quality reports"
authors:
- Anthropic
organisation: Anthropic
source_type: blog
venue: Anthropic Engineering
url: https://www.anthropic.com/engineering/april-23-postmortem
year: 2026
date_published: 2026-04-23
anthropic: true
topic:
- topic/claude-code
- topic/best-practices
tags:
- claude-code
- postmortem
- reasoning-effort
- prompt-caching
- system-prompt
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-engineering
af_targets:
- af:RSCH-01/claude-code
- af:RSCH-04/Q12
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 650679fefb8b9a5712ad089e94b63d804a74c60f9457680a95d72f284fbe49b4
---

# An update on recent Claude Code quality reports

> Anthropic, "An update on recent Claude Code quality reports", Anthropic Engineering, 23 April 2026, https://www.anthropic.com/engineering/april-23-postmortem.

## Summary

Anthropic's postmortem explains why Claude Code seemed less capable between early March and mid-April 2026, with users reporting lower intelligence, forgetfulness, repetition and faster usage-limit depletion. It traces the reports to three separate changes: the default reasoning effort moved from high to medium on 4 March to cut latency; a prompt-caching optimisation on 26 March cleared thinking history on every turn instead of once; and a system prompt instruction on 16 April capped text between tool calls and in final responses. All three were reverted or fixed by 20 April (v2.1.116), and usage limits were reset for affected subscribers.

## Key Concepts

- Product quality in an agent harness depends on defaults and prompts as much as on the model.
- Three small, individually reasonable changes compounded into a broad regression.
- A caching bug can silently remove reasoning context and make an agent look forgetful.
- Verbosity limits in a system prompt can reduce coding quality.

## Terminology

- Reasoning effort: the setting controlling how much the model thinks before answering.
- Thinking history: prior reasoning retained across turns in a session.
- Soak period: time a change runs before wide release.

## Architecture and Implementation

The report describes harness-level levers: a default effort level, a prompt-caching layer that manages thinking history, and a system prompt with length instructions. The fixes were reversions of each lever to its prior behaviour.

## Code Examples

The source carries no reusable code.

## Best Practices

- Test with public builds, not only internal versions.
- Run broader per-model evaluations for every system prompt change.
- Add soak periods and gradual rollouts for changes that can affect intelligence.
- Improve code review tooling for harness changes.

## Warnings and Anti-Patterns

- Trading intelligence for latency by default without user signal.
- Shipping a prompt or cache change without per-model evaluation.
- Testing only on internal builds that differ from what users run.

## Related Concepts

- [[claude-code]]
- [[evaluation]]
- [[prompt-engineering]]

## Future Work

Anthropic commits to wider internal testing on public builds, more evaluation per prompt change and gradual rollouts.

## References

- https://www.anthropic.com/engineering/april-23-postmortem
