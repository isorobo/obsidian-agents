---
type: source
status: draft
created: 2026-07-11
title: "Prompt Engineering in 2026: Techniques That Work"
authors:
- AI Builder Club
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 3.9
url: https://www.aibuilderclub.com/blog/prompt-engineering-guide-2026
year: 2026
date_published: 2026-04-16
anthropic: false
topic:
- topic/prompt-engineering
tags:
- prompt-engineering
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
af_targets:
- none
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: a3ccc3880dab5e12f4cea14a9ab0273d80241218798b640b1fd11febfc4d1f1d
---

# Prompt Engineering in 2026: Techniques That Work

> AI Builder Club, "Prompt Engineering in 2026: Techniques That Work", Build AI Agents Course, 16 April 2026, https://www.aibuilderclub.com/blog/prompt-engineering-guide-2026.

## Summary

The lesson treats prompt engineering as a learnable, principle-based skill rather than an intuitive knack, anchored on one mental model it calls the Door Rule: the model only knows what is in the context window, as if an expert walked into a sealed room with no memory of anything said before. Most prompt failures, on this framing, are missing-context failures, not reasoning failures — and the fix is a structured prompt (role, task, context, output format) iterated over three to five cycles rather than a single clever phrasing.

## Key Concepts

- The Door Rule: the model has no access to anything outside the current context window, so every prompt failure traces back to some piece of missing context the writer assumed was obvious.
- A well-formed prompt has four parts: role/persona (sets tone and vocabulary), task (a specific action verb — write, summarise, refactor, extract), context (actual text, code, or data, not a description of it), and output format (JSON, bullets, a table, a single sentence).
- Four core techniques: chain-of-thought prompting for multi-step logic, two-to-three few-shot examples to teach a pattern faster than instructions alone, explicit negative instructions (stating what not to do, such as no introduction or disclaimer), and constrained output (hard word or character limits rather than a vague request for brevity).
- Model selection should match task complexity: fast, cheap models for classification and extraction; reasoning models for logic and planning; matching the two the wrong way wastes money without buying accuracy.

## Terminology

- Door Rule — the framing that a model has no memory or awareness beyond its current context window, used as the default diagnostic for a failing prompt.
- Chain of thought — prompting the model to work through a problem step by step before giving a final answer, improving multi-step logical accuracy.
- Constrained output — specifying a hard limit (word count, character count, format) rather than a soft, subjective instruction like "keep it brief."

## Architecture and Implementation

Three structured output patterns are named: JSON Schema for programmatic parsing, XML tags separating reasoning from the final answer for easier debugging, and explicit Markdown formatting (headers, bullets, bold, code blocks) for human-facing output. The lesson gives three before/after prompt rewrites (a vague summarisation request tightened to three bullets on practical implications, a vague simplification request tightened to a stated reading level and sentence length, and a vague editing request tightened to a word cap and tone) as worked demonstrations of the four-part structure in practice. Model selection is given as a table matching task type to model tier: fast/cheap models for extraction, general-purpose models for everyday tasks, reasoning models for logic and planning, and long-context or real-time-voice models for their respective specialised cases.

## Code Examples

None as runnable code; the lesson's worked examples are before/after prompt text rather than program code.

## Best Practices

- Apply the Door Rule as the first diagnostic whenever a prompt produces a bad result: what context did the model need that it did not have.
- Use two to three few-shot examples to teach a pattern rather than relying on instructions alone to convey it.
- State negative instructions explicitly (what not to include) rather than assuming the model will infer an omission is wanted.
- Set hard, measurable output constraints (word counts, formats) instead of soft, subjective ones.
- Match model tier to task complexity rather than defaulting to the most capable available model for every call.

## Warnings and Anti-Patterns

- Treating a prompt like a casual search query, rather than a detailed instruction for a system with no persistent context, is named as the root cause of most prompt failures.
- Using a reasoning-tier model for simple classification or extraction wastes cost without buying accuracy the task did not need.
- Expecting a single prompt attempt to succeed, rather than budgeting three to five iteration cycles, sets an unrealistic bar for first-draft prompt quality.

## Related Concepts

- [[prompt-engineering]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson's own exercises point toward applying the same structure to a structured JSON extraction pipeline as the natural next step after mastering single-turn prompt rewriting.

## References

- Prompt Engineering in 2026: Techniques That Work — https://www.aibuilderclub.com/blog/prompt-engineering-guide-2026
