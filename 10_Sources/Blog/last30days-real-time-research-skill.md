---
type: source
status: draft
created: 2026-07-11
title: "last30days-skill: Real-Time Research for AI Agents"
authors:
- Jason Zhou
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 3.12
url: https://www.aibuilderclub.com/blog/last30days-skill-real-time-research
year: 2026
date_published: 2026-06-09
anthropic: false
topic:
- topic/tool-use
- topic/agent-skills
tags:
- research
- agent-skills
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
---

# last30days-skill: Real-Time Research for AI Agents

> Jason Zhou, "last30days-skill: Real-Time Research for AI Agents", AI Builder Club, Build AI Agents Course, 9 June 2026, https://www.aibuilderclub.com/blog/last30days-skill-real-time-research.

## Summary

`last30days-skill` is a community-built agent skill that searches Reddit, X, YouTube, Hacker News, Polymarket, GitHub, TikTok, Instagram, and Bluesky in parallel and synthesises the results into a ranked brief by actual engagement rather than editorial ranking. The lesson frames its appeal as closing a real fragmentation gap: no single mainstream AI platform can search across all of those surfaces at once, so an agent that can bridges a genuine blind spot rather than duplicating an existing capability.

## Key Concepts

- Cross-platform synthesis is the core mechanism: the skill queries multiple community platforms in parallel and merges the results into one ranked brief, rather than returning separate per-platform results.
- Four sources (Reddit, Hacker News, Polymarket, GitHub) work immediately with no configuration; the remaining five (X, YouTube, TikTok, Instagram, Bluesky) require a roughly thirty-second setup wizard.
- Version 3.3 added intelligent pre-search (resolving handles, repos, and subreddits before the actual query), cross-source clustering of duplicate stories, shareable HTML briefs, an engagement-based "best takes" ranking pass, and single-pass comparisons that the lesson reports cutting a multi-entity comparison from roughly twelve minutes to three.
- The skill installs the same way across Claude Code (via a plugin marketplace) and thirty-plus other agent hosts (via `npx skills add`), following the same distribution pattern as 3.11's `google/skills`.

## Terminology

- Cross-source clustering — merging near-duplicate stories that appear on multiple platforms into a single result, rather than surfacing each platform's copy separately.
- Engagement-based ranking — ordering results by actual community response (upvotes, replies, virality) rather than by search-engine relevance scoring.

## Architecture and Implementation

Installation in Claude Code runs through `/plugin marketplace add mvanhorn/last30days-skill` followed by `/plugin install last30days`; other hosts use `npx skills add mvanhorn/last30days-skill -g`. A worked example query, `/last30days Andrej Karpathy`, returns recent tweets, commits, and YouTube appearances synthesised into one brief. Named use cases include pre-meeting research on a named person, side-by-side competitive sentiment comparisons, fast-moving topic monitoring, and general real-time fact-finding beyond a model's training cutoff.

## Code Examples

None as runnable code; the lesson documents CLI installation commands and example query syntax rather than a program.

## Best Practices

- Complete the roughly thirty-second setup wizard for the five configuration-requiring platforms rather than settling for the four zero-config sources if broader coverage is the goal.
- Use the skill specifically to close the knowledge-cutoff gap — recent community sentiment and activity — rather than as a general substitute for a model's own reasoning.

## Warnings and Anti-Patterns

None specific to this lesson; general search-tool caveats (source reliability, platform-specific bias in what surfaces as "engaging") apply but are not addressed directly in the extracted content.

## Related Concepts

- [[tool-use]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson closes with a practical suggestion rather than an open question: test the skill against familiar topics first, to calibrate how its community-engagement ranking compares against personal assumptions before relying on it for unfamiliar ones.

## References

- last30days-skill: Real-Time Research for AI Agents — https://www.aibuilderclub.com/blog/last30days-skill-real-time-research
