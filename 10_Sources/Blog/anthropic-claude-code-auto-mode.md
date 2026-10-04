---
type: source
status: draft
created: 2026-10-04
title: "How we built Claude Code auto mode: a safer way to skip permissions"
authors:
- John Hughes
organisation: Anthropic
source_type: blog
venue: Anthropic Engineering
url: https://www.anthropic.com/engineering/claude-code-auto-mode
year: 2026
date_published: 2026-03-25
anthropic: true
topic:
- topic/claude-code
- topic/security
- topic/tool-use
tags:
- claude-code
- auto-mode
- permissions
- classifier
- prompt-injection
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-engineering
af_targets:
- af:ADR-0007
- af:ADR-0004
- af:RSCH-04/Q28
- af:RSCH-04/Q26
- af:RSCH-01/claude-code
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 37e1e9b537e61cf0cf1d4f26aedd1c1d89c040bdd4e939e5bef435e5b47b60b5
---

# How we built Claude Code auto mode: a safer way to skip permissions

> John Hughes, "How we built Claude Code auto mode: a safer way to skip permissions", Anthropic Engineering, 25 March 2026, https://www.anthropic.com/engineering/claude-code-auto-mode.

## Summary

The post explains auto mode in Claude Code, which replaces many manual permission prompts with automated checks to reduce approval fatigue. It uses two layers: a server-side prompt-injection probe that screens tool outputs before they enter context, and a transcript classifier (running on Sonnet 4.6) that judges actions before execution in two stages, a fast single-token filter then chain-of-thought only when flagged. On 10,000 real traffic samples the full pipeline had a 0.4% false-positive rate and a 17% false-negative rate on real overeager actions, which the authors present as an honest trade-off.

## Key Concepts

- Threat model with four failure modes: overeager behaviour, honest mistakes, prompt injection and misalignment.
- Three permission tiers: a safe-tool allowlist, in-project file operations, and classifier review for high-risk actions.
- The classifier sees user messages and tool calls only; assistant text and tool results are stripped to resist manipulation.
- Judge the real-world impact of an action, not its surface syntax.

## Terminology

- False positive rate and false negative rate of the classifier.
- Approval fatigue: reduced attention caused by excess prompts.
- Scope escalation: acting beyond authorised boundaries.
- Deny-and-continue: after a block the agent retries a safer approach, up to 3 consecutive or 20 total denials.

## Architecture and Implementation

A fixed prompt template has three user-customisable slots: environment trust boundaries, block rules and allow exceptions. Running `claude auto-mode defaults` shows the baseline rules. Blanket permission rules such as arbitrary shell access or wildcarded interpreters are dropped on entering auto mode.

## Code Examples

The source carries no reusable code beyond the `claude auto-mode defaults` command.

## Best Practices

- Start from the defaults and edit rather than write rules from scratch.
- Use auto mode where approval overhead exceeds marginal safety value.
- Keep human review for high-stakes infrastructure.

## Warnings and Anti-Patterns

- A 17% false-negative rate means some dangerous actions pass.
- Stripping tool results removes provenance, so the classifier cannot verify where a value came from.
- Existing blanket allow rules may stop working.
- Rare false positives still force retries on long tasks.

## Related Concepts

- [[claude-code]]
- [[tool-use]]
- [[workflow-vs-autonomous-agent]]

## Future Work

The authors treat the false-negative rate as the main area to improve.

## References

- https://www.anthropic.com/engineering/claude-code-auto-mode
