---
type: source
status: draft
created: 2026-07-11
title: "Karpathy's Software 3.0: The Context Window Is Code"
authors:
- AI Builder Club
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 1.11 (commentary on Andrej Karpathy's Sequoia Ascent 2026 talk)
url: https://www.aibuilderclub.com/blog/karpathy-software-3-0
year: 2026
date_published: 2026-05-27
anthropic: false
topic:
- topic/foundations
- topic/karpathy
tags:
- karpathy
- software-3.0
- agent-native
- course
nlm_id:
nlm_skip: false
watchlist_channel:
af_targets:
- af:ADR-0008
- af:RSCH-04/Q12
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 29de5b1ce90f9708f52a678d8306949aff99cdd03d913c57ee65582d1f5f2a16
---

# Karpathy's Software 3.0: The Context Window Is Code

> AI Builder Club, "Karpathy's Software 3.0: The Context Window Is Code", Build AI Agents Course, 27 May 2026, https://www.aibuilderclub.com/blog/karpathy-software-3-0. AI Builder Club's commentary on Andrej Karpathy's Sequoia Ascent 2026 talk, not Karpathy's original essay.

## Summary

Karpathy frames three eras of software: 1.0 is explicit deterministic code, 2.0 is network weights trained rather than written, and 3.0 is the context window itself as the program, with the LLM as its interpreter. The lesson stresses this is a categorical shift, not faster coding, and gives a working vetting framework: AI capability improves fastest where a domain offers automatic, verifiable success signals, which is why coding agents move faster than agents in less verifiable domains.

## Key Concepts

- Software 3.0 — the context window is the program; the scarce resource shifts from lines of code to context design.
- Traditional software automates what you can specify; LLMs and reinforcement learning automate what you can verify — a different production function entirely.
- Karpathy's capability formula: capability spike is a function of verifiability, training attention, data coverage, and economic value.
- Agent-native infrastructure means building the machine-facing version of a product — Markdown docs, CLIs, APIs, MCP servers, structured logs — as a first-class target, not an afterthought to the human-facing UI.

## Terminology

- Software 1.0 — explicit, deterministic code, brittle at the edges of what was anticipated.
- Software 2.0 — machine learning: the trained network's weights become the program.
- Software 3.0 — the context window functions as the program; the LLM interprets it at run time.
- Verifiability — whether a domain offers an automatic pass/fail or scoreable success signal (tests passing, a program compiling) that lets a model iterate fast.

## Architecture and Implementation

The MenuGen example contrasts a traditional multi-service stack (photo upload, OCR, image generation, UI rendering) against a Software 3.0 version collapsed into a single multimodal prompt that overlays dish images on a menu photo directly — "the entire app architecture disappears." The OpenClaw installation example contrasts a traditional shell script, fragile across environments, against a Software 3.0 setup where a text block handed to an agent reads the environment, debugs errors iteratively, and completes an adaptive install. The LLM Wiki example — treated in full in [[10_Sources/Blog/karpathy-llm-wiki-pattern|the companion lesson]] — is cited here as a capability that has no robust classical-software equivalent at all: no traditional program can maintain a synthesised, cross-linked knowledge base over messy human documents the way an LLM can.

## Code Examples

None. The lesson is conceptual, illustrated through the MenuGen and OpenClaw worked examples rather than code.

## Best Practices

- Before optimising an existing workflow, ask which workflows become possible for the first time under Software 3.0, not just which get faster.
- Identify the verifiable structure inside a domain — what can be tested, measured, or scored — and build there first; that is where AI improves fastest.
- Design every product decision with two versions in mind, the human version and the agent version, and give the agent version real priority.
- Use Karpathy's five vetting questions as a practical filter for 2026 product decisions, not a rhetorical exercise: what becomes possible with an agent as primary user; what rebuilds around sensors, actuators, and verifiable loops; what software should disappear into a direct model transform; what verifiable domains remain undertrained by frontier labs; and what judgment must stay human to preserve quality.

## Warnings and Anti-Patterns

- Treating Software 3.0 as an incremental speed gain over existing workflows misses the categorical shift Karpathy is describing.
- Building agent-facing infrastructure as an afterthought to a human-facing UI cedes the actual growth surface.
- The traditional automate-what-you-specify mental model does not transfer to a domain where success is defined by verification rather than specification.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[agent-vs-llm]]
- [[claude-code]]
- [[20_People/andrej-karpathy/profile|Andrej Karpathy]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson gestures at a longer-term extrapolation — neural networks as host processes, CPUs as coprocessors, the current application layer dissolving — but explicitly frames this as years away and out of scope for the present analysis.

## References

- Karpathy's Software 3.0: The Context Window Is Code — https://www.aibuilderclub.com/blog/karpathy-software-3-0
