---
type: person
status: stub
created: 2026-07-11
name: Andrej Karpathy
slug: andrej-karpathy
kind: person
role: Independent AI researcher and educator; former Director of AI, Tesla; founding member, OpenAI
affiliations: [OpenAI, Tesla, Eureka Labs]
topic:
- topic/karpathy
- topic/best-practices
tags: [karpathy, agentic-engineering, software-3.0]
key_sources: ["[[10_Sources/Blog/karpathy-agentic-engineering-framework|Agentic Engineering: Karpathy's New Framework]]"]
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 89bf5a9d5773e53cc1f169e3aa38373fc1062f5b8c92c44b1481608952b252c1
---

# Andrej Karpathy

> Andrej Karpathy names and frames recurring ideas in agent engineering — vibe coding versus agentic engineering, Software 3.0, the LLM wiki pattern — that the field then adopts as shared vocabulary.

## Role

Andrej Karpathy is an independent AI researcher and educator. He co-founded OpenAI, led Tesla Autopilot's computer-vision effort as Director of AI, and later founded Eureka Labs. His 2026 public talks and posts, most prominently an April 2026 Sequoia Ascent talk, set terms the wider agent-engineering community now uses without attribution.

## Contribution to Agent Engineering

- **Agentic engineering versus vibe coding** — draws the line between low-oversight AI-assisted coding and a disciplined practice of spec design, diff review, eval design, security oversight, and taste. See [[10_Sources/Blog/karpathy-agentic-engineering-framework|the framework note]].
- **Software 3.0** — frames the context window as the program and the LLM as its interpreter, alongside Software 1.0 (explicit code) and Software 2.0 (network weights). See [[10_Sources/Blog/karpathy-software-3-0|the Software 3.0 note]].
- **Verifiability as the capability wedge** — proposes that AI capability improves fastest where a domain offers automatic, verifiable success signals, which explains why coding agents outpace agents in less verifiable domains.
- **The LLM wiki pattern** — proposes a three-layer system (raw sources, an LLM-maintained wiki, a schema file) where the model owns bookkeeping that defeats human-maintained wikis. This is the pattern this vault, `wiki-agents`, itself implements. See [[10_Sources/Blog/karpathy-llm-wiki-pattern|the LLM wiki note]].
- **agents.md** — public statements on agent permission boundaries, auditability, and fail-loud design, synthesised by third parties (not yet published by Karpathy himself as a formal document at time of writing). See [[10_Sources/Blog/karpathy-agents-md-framework|the agents.md commentary note]].

## Key Positions

- Speed without architectural review produces plausible-but-wrong systems; oversight scales with the reversibility of an action, not the complexity of the task.
- As agents absorb code generation, human understanding, taste, eval design, and agent orchestration become the scarce, valuable skills.
- Software that can be reduced to a single well-designed prompt should stop existing as multi-service software.

## Timeline

- 2026-04 — Sequoia Ascent talk on agentic engineering and vibe coding; publishes the LLM wiki gist.
- 2026-05 — Software 3.0 talk and commentary track published by third parties, including AI Builder Club.
- 2026-06 — Public statements synthesised into an agents.md commentary by third parties.

## Status

This profile is a stub. It is built entirely from third-party commentary (AI Builder Club) on Karpathy's public talks and posts, not from his primary essays or transcripts directly. A future run should source his original Sequoia Ascent transcript and the LLM wiki gist directly.

## Key Sources

- [[10_Sources/Blog/karpathy-agentic-engineering-framework|Agentic Engineering: Karpathy's New Framework]]
- [[10_Sources/Blog/karpathy-agents-md-framework|Karpathy's agents.md: What It Is and Why It Matters]]
- [[10_Sources/Blog/karpathy-software-3-0|Karpathy's Software 3.0: The Context Window Is Code]]
- [[10_Sources/Blog/karpathy-llm-wiki-pattern|Karpathy's LLM Wiki: A Knowledge Base That Compounds]]

## Related

- [[20_People/ai-builder-club/profile|AI Builder Club]]
- [[what-is-an-ai-agent]]
- [[best-practices-index]]

## See also

- [[MOC - Karpathy]]
