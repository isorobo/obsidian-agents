---
type: release
status: draft
created: 2026-10-04
title: "Introducing Claude Fable 5.1 and Claude Mythos 5.1"
organisation: Anthropic
source_type: release-note
product: Claude Fable 5.1
version: claude-fable-5-1
url: https://www.anthropic.com/claude-fable-and-mythos-5-1
year: 2026
date_published: 2026-09-01
anthropic: true
topic:
- topic/release-notes
- topic/security
tags:
- claude-fable-5-1
- claude-mythos-5-1
- model-release
- safeguards
watchlist_channel: anthropic-news
af_targets:
- af:ADR-0003
- af:ADR-0007
- af:RSCH-04/Q29
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 5d0f97fe7ffe3e06c49d83bb98b90b482c35b87352b68fc54a8a7652adfabf8a
---

# Introducing Claude Fable 5.1 and Claude Mythos 5.1

> Claude Fable 5.1 (`claude-fable-5-1`) and Claude Mythos 5.1, September 2026 (listed 1 September 2026).

## Summary

Anthropic announced two models. Claude Fable 5.1 is generally available on the Claude API, AWS, Google Cloud and Microsoft Azure. Claude Mythos 5.1 is limited to vetted US organisations through the Cyber Verification Program and the Life Sciences Verification Program. Fable 5.1 is priced at $10 input and $50 output per million tokens, with cache reads at $0.25 (a 75 percent cut). Anthropic estimates about 25 percent savings on typical workloads and up to about 45 percent on highly agentic tasks. Reported results include 55.8 percent (Fable) and 60.9 percent (Mythos) on Terminal-Bench 4.0.

## New Capabilities

- Enterprise Frontier Safeguards: zero data retention with customer-controlled cloud infrastructure.
- Biology safeguards with 85 percent fewer false positives on benign requests.
- Cybersecurity safeguards with about 60 percent fewer interventions, now permitting vulnerability discovery but not exploit development.
- Stronger anti-distillation mechanisms that block manual context editing for new API accounts.
- EU AI Act support through invisible text watermarking and a detection API in private preview.

## Deprecated Features

- None stated. Manual context editing is blocked for new API accounts.

## Migration Notes

New API accounts cannot edit context manually, so agents that rewrite prior reasoning turns need a different approach. Mythos 5.1 access requires approval into a verification programme. The announcement does not state a context window.

## Engineering Implications

Cache read pricing cuts the cost of long agent runs that reuse context. Safeguard changes alter refusal behaviour in security and biology agents, so evaluate those workloads again. Restricted access to Mythos means a design that assumes it must degrade to Fable. Blocked context editing constrains harnesses that prune or rewrite history, which bears on how memory and context are managed.

## Practical Examples

```text
# The source shows no reusable code. The API identifier is claude-fable-5-1.
```

## Related

- [[claude-agent-sdk]]
- [[tool-use]]
- [[memory]]

## References

- https://www.anthropic.com/claude-fable-and-mythos-5-1

## See also

- [[MOC - Release Notes]]
