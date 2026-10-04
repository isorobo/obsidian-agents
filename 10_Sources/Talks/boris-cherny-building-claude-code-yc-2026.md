---
type: source
status: stub
created: 2026-10-04
title: "Boris Cherny: Building Claude Code"
authors:
- Boris Cherny
- Diana Hu
organisation: Y Combinator
source_type: talk
venue: Y Combinator Startup Podcast
url: https://www.ycombinator.com/library/UN-boris-cherny-building-claude-code
year: 2026
date_published: 2026-07-28
anthropic: false
topic:
- topic/boris-cherny
- topic/prompt-engineering
- topic/security
tags:
- claude-code
- system-prompt
- harness
- opus-5
- auto-mode
nlm_id:
nlm_skip: false
watchlist_channel: boris-cherny
af_targets:
- cf:adapter/claude-code
- af:RSCH-04/Q05
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: ea89bf3c60524ef68d8741aa6eec429a0d603bb8c2d7fb1f199c0cb0e976eae8
---

# Boris Cherny: Building Claude Code

> Boris Cherny and Diana Hu, "Boris Cherny: Building Claude Code", Y Combinator Startup Podcast, 28 July 2026, https://www.ycombinator.com/library/UN-boris-cherny-building-claude-code.

## Summary

Boris Cherny, who leads Claude Code at Anthropic, talks with Diana Hu of Y Combinator about what the newest models can do and how that changes the way Claude Code is built. The YC library page itself returned only a title when fetched, so this note rests on a third-party transcript page (spoken.md) for the same episode and is marked as a stub. The central point is that a stronger model needs less corrective scaffolding: the latest Claude Code release removed about 80 percent of the system prompt because much of it corrected behaviour the model now gets right unaided.

## Key Concepts

- Product and model move together: tools, prompts and system instructions are revisited with each model release.
- Scaffolding has an expiry date. Prompt text written to fix a weakness in one model may not carry over to the next.
- Longer autonomous runs (the speaker says days to months) change what a harness must support.
- Safety is layered: alignment work, interpretability research and classifier-based auto mode, validated by red-teaming.

## Terminology

- System prompt: the standing instructions Claude Code sends with each request.
- Auto mode: a classifier-gated permission mode for running without per-action approval.
- Harness: the tools, prompts and controls wrapped around the model.

## Architecture and Implementation

The transcript describes no code-level architecture. The implementation lesson is subtractive: when a new model ships, test whether each prompt rule still earns its place and delete those that do not.

## Code Examples

The source carries no reusable code.

## Best Practices

- Re-evaluate the system prompt on every model change instead of only adding to it.
- Treat prompt rules as hypotheses about model weakness, and retire them when the weakness goes.
- Combine model-level alignment with runtime classifiers rather than relying on either alone.

## Warnings and Anti-Patterns

- Carrying old prompt scaffolding forward unchanged can add noise or cost without benefit.
- Prompt injection is described as reduced by alignment plus classifiers, not eliminated by prompt text.

## Related Concepts

- [[claude-code]]
- [[prompt-engineering]]
- [[20_People/boris-cherny/profile|Boris Cherny]]

## Future Work

The talk points to agents running for far longer periods and to further model-driven simplification of the harness.

## References

- Boris Cherny: Building Claude Code, Y Combinator library, https://www.ycombinator.com/library/UN-boris-cherny-building-claude-code
- Transcript mirror used for grounding: https://spoken.md/episode/boris-cherny-building-claude-code-1000778651350
