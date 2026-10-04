---
type: release
status: draft
created: 2026-10-04
title: "Introducing Claude Sonnet 5.5"
organisation: Anthropic
source_type: release-note
product: Claude Sonnet 5.5
version: claude-sonnet-5-5
url: https://www.anthropic.com/claude-sonnet-5-5
year: 2026
date_published: 2026-09-28
anthropic: true
topic:
- topic/release-notes
tags:
- claude-sonnet-5-5
- model-release
- pricing
- preserved-thinking
watchlist_channel: anthropic-news
af_targets:
- af:ADR-0003
- af:RSCH-04/Q29
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: a56f344fca3a5b6e87f943cb77199a9432933c5b833c72b7a5383db6211b7356
---

# Introducing Claude Sonnet 5.5

> Claude Sonnet 5.5, model id `claude-sonnet-5-5`, 28 September 2026.

## Summary

Anthropic released Claude Sonnet 5.5 on 28 September 2026 on the Claude Platform, the Claude apps, AWS, Google Cloud and Microsoft Azure. Per-token pricing is unchanged from Sonnet 5 at $2 input and $10 output per million tokens, but Anthropic reports up to 30 percent lower cost per task and over 30 percent faster output. Reported results include 70.6 percent on Terminal-Bench 4.0, 46.2 percent on FrontierCode 1.1 at Max effort, 55.5 percent on CursorBench 4.0 and 80.1 percent (partial credit) on OSWorld 2.1.

## New Capabilities

- Cache reads $0.20 and cache writes $2.50 per million tokens.
- Expanded preserved thinking.
- Cybersecurity safeguards similar to Opus 5.5, plus classifiers that block extraction of reasoning (distillation protection).
- GDPval-AA v2.1 score of 1844, close to Opus 5.5 at 1846.

## Deprecated Features

- Thinking-off configurations no longer work as before: they require the new `between_tools` setting.

## Migration Notes

Anyone running Sonnet with thinking disabled must move to the `between_tools` setting before upgrading to `claude-sonnet-5-5`. Re-run tool-use and agentic evaluations first, since token use per task shifts.

## Engineering Implications

Near-Opus agentic quality at Sonnet pricing makes Sonnet 5.5 the default candidate for high-volume agent loops, with Opus kept for the hardest steps. Per-task cost, not per-token price, is the figure to track. The thinking-off change can break existing harness configuration, so pin the model id and gate upgrades behind an evaluation run. Distillation protection may limit how reasoning traces can be stored or replayed.

## Practical Examples

```text
# The source shows no reusable code. The model id is claude-sonnet-5-5.
```

## Related

- [[claude-code]]
- [[claude-agent-sdk]]
- [[tool-use]]

## References

- https://www.anthropic.com/claude-sonnet-5-5

## See also

- [[MOC - Release Notes]]
