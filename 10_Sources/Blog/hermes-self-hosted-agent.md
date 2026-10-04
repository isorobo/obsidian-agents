---
type: source
status: draft
created: 2026-07-11
title: "Hermes Agent: Self-Hosted AI That Never Forgets You (2026)"
authors:
- Jason Zhou
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 2.3
url: https://www.aibuilderclub.com/blog/hermes-nous-research-self-improving-agent
year: 2026
date_published: 2026-06-02
anthropic: false
topic:
- topic/memory
tags:
- self-hosted
- nous-research
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
af_targets:
- af:ADR-0005
- af:RSCH-04/Q11
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 2012ab74f7bf303c981067cb6493e6f848f51e2ea275c67c258e31e45f789671
---

# Hermes Agent: Self-Hosted AI That Never Forgets You (2026)

> Jason Zhou, "Hermes Agent: Self-Hosted AI That Never Forgets You (2026)", Build AI Agents Course, 2 June 2026, https://www.aibuilderclub.com/blog/hermes-nous-research-self-improving-agent.

## Summary

Hermes is Nous Research's self-hosted agent, profiled here as a case study in what a session-based tool like Claude Code cannot do on its own: persist memory across sessions, run scheduled work while the user is offline, and turn its own repeated multi-step work into reusable skill files. The lesson frames Hermes and Claude Code as complementary rather than competing — one excels at focused, single-project coding, the other adds cross-project memory, background scheduling, and provider flexibility, and the two can even compose, with Hermes spawning Claude Code sessions as subagents.

## Key Concepts

- A three-tier memory architecture: Tier 1 (`USER.md`/`MEMORY.md`) loads deterministically every session; Tier 2 is searchable SQLite history with LLM summarisation; Tier 3 optionally connects external providers.
- Deterministic Tier 1 retrieval is presented as a deliberate contrast to purely probabilistic vector search — guaranteed context beats "probably relevant" context for the facts that must never drop.
- Self-improving skills: the agent encodes frequently repeated multi-step tasks as local Markdown skill files, which the lesson explicitly frames as drafts requiring human review, not autonomous production code.
- A built-in scheduler runs recurring background workflows (monitoring issues, generating digests) and delivers results to messaging apps without the user present — the asynchronous layer the lesson says session-based tools lack.

## Terminology

- Self-hosted agent — an agent run and persisted entirely on infrastructure the user controls, as opposed to a hosted session tied to one provider.
- Self-improving skill — a Markdown file the agent generates from its own repeated task execution, intended for human review before production use.

## Architecture and Implementation

Setup uses a one-line install script (roughly 15 minutes), OAuth or API-key provider configuration, and Docker images for both amd64 and arm64. The project integrates with 16-plus messaging platforms and multiple LLM providers. The lesson cites internal benchmarks claiming agents that have accumulated 20-plus self-created skills complete tasks roughly 40% faster than a fresh instance, though it does not independently verify that figure.

## Code Examples

None; the lesson is a product walkthrough (installation script, configuration steps, and a comparison table against Claude Code) rather than a code tutorial.

## Best Practices

- Review every auto-generated skill file before allowing it to run unattended in production.
- Put self-hosted instances behind authentication and a VPN or SSH tunnel before handling sensitive workflows.
- Treat the project as "maturing" rather than fully production-hardened for mission-critical use.

## Warnings and Anti-Patterns

- Auto-generated skills are drafts, not verified procedures; running them unreviewed risks repeating a flawed approach at scale.
- Rapid adoption and star count are not, on their own, evidence of production readiness for sensitive or mission-critical workflows.

## Related Concepts

- [[memory]]
- [[claude-code]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson does not propose a next step beyond noting the Hermes-spawns-Claude-Code composition pattern as "interesting" without a worked example.

## References

- Hermes Agent: Self-Hosted AI That Never Forgets You (2026) — https://www.aibuilderclub.com/blog/hermes-nous-research-self-improving-agent
