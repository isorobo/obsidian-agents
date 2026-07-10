---
type: release
status: draft
created: 2026-07-10
title: Introducing Claude Sonnet 5
organisation: Anthropic
source_type: release-note
product: Claude Sonnet 5
version: claude-sonnet-5
url: https://www.anthropic.com/news/claude-sonnet-5
date_published: 2026-06-30
anthropic: true
topic:
- topic/release-notes
tags: [claude-sonnet-5, model-release, agentic, pricing, tool-use]
---

# Introducing Claude Sonnet 5

> Claude Sonnet 5, model id `claude-sonnet-5`, released 30 June 2026.

## Summary

Anthropic released Claude Sonnet 5 on 30 June 2026. The model targets agentic coding, tool use, reasoning, and knowledge work at lower cost. Performance approaches Claude Opus 4.8. Anthropic calls it the most agentic Sonnet model, able to plan, use browsers and terminals, and run autonomously. Sonnet 5 became the default model for the Free and Pro tiers on release.

## New Capabilities

- Agentic search on BrowseComp matches or exceeds Sonnet 4.6 across effort levels.
- Computer use on OSWorld-Verified moves toward Opus 4.8.
- Reasoning, tool use, and coding improve over Sonnet 4.6.

## Deprecated Features

- None stated. Sonnet 4.6 remains available for existing integrations.

## Migration Notes

Point the API to the model id `claude-sonnet-5`. Test tool-use and agentic flows against the new model before switching production traffic. Introductory pricing runs through 31 August 2026 at $2 per million input tokens and $10 per million output tokens. Standard pricing then moves to $3 per million input tokens and $15 per million output tokens.

## Engineering Implications

Sonnet 5 brings near-Opus agentic performance at a Sonnet price. An agent that ran on Opus for browser and terminal work may run on Sonnet 5 for less. Lower token cost widens the budget for long, tool-heavy runs. The model reaches the Claude API, Claude Code, and the Claude Platform.

## Practical Examples

```python
from anthropic import Anthropic

client = Anthropic()
message = client.messages.create(
    model="claude-sonnet-5",
    max_tokens=1024,
    messages=[{"role": "user", "content": "Plan and run an agentic search task."}],
)
print(message.content)
```

## Related

- [[claude-code]]
- [[claude-agent-sdk]]
- [[tool-use]]

## References

- https://www.anthropic.com/news/claude-sonnet-5
- https://platform.claude.com/docs/en/about-claude/models/overview

## See also

- [[MOC - Release Notes]]
