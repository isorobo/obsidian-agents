---
type: source
status: draft
created: 2026-10-04
title: "Generative Agents: Interactive Simulacra of Human Behavior"
authors:
- Joon Sung Park
- Joseph C. O'Brien
- Carrie J. Cai
- Meredith Ringel Morris
- Percy Liang
- Michael S. Bernstein
organisation: Stanford University and Google Research
source_type: paper
venue: arXiv
url: https://arxiv.org/abs/2304.03442
year: 2023
date_published: 2023-04-07
anthropic: false
topic:
- topic/memory
- topic/research-papers
tags:
- generative-agents
- memory-stream
- reflection
- planning
- simulation
nlm_id:
nlm_skip: false
watchlist_channel: af-corpus-papers
af_targets:
- af:RSCH-01/generative-agents
- af:RSCH-04/Q11
- af:RSCH-04/Q12
- af:RSCH-04/Q09
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 889d366373517ae02242bf8d1e9f3df4c7b9a38446cb78931f48d75f8da80103
---

# Generative Agents: Interactive Simulacra of Human Behavior

> Joon Sung Park, Joseph C. O'Brien, Carrie J. Cai, Meredith Ringel Morris, Percy Liang and Michael S. Bernstein, "Generative Agents: Interactive Simulacra of Human Behavior", arXiv, 7 April 2023, https://arxiv.org/abs/2304.03442.

## Summary

The paper presents computational agents that simulate believable human behaviour by combining large language models with an architecture for memory. The architecture lets an agent keep a record of experience in natural language, synthesise that record into higher-level reflections, and retrieve memories dynamically to plan. The authors place twenty-five agents in an interactive sandbox inspired by The Sims. From a single user-specified goal about a Valentine's Day party, the agents spread invitations, formed new relationships and coordinated attendance over two days. Ablations showed that observation, planning and reflection each contribute significantly to believability. This note is based on the arXiv abstract page (v1 April 2023, v2 August 2023); the full text was not read.

## Key Concepts

- Natural-language experience record that the agent accumulates as it observes.
- Reflection: synthesising raw records into higher-level inferences.
- Dynamic retrieval of memories to drive planning.
- Emergent social behaviour from one seed goal.
- Ablation evidence that all three components (observe, plan, reflect) matter.

## Terminology

- Generative agent: an LLM-backed agent with memory, reflection and planning that simulates human behaviour.
- Reflection: a synthesis step that turns experience into reusable conclusions.
- Simulacra: the believable behavioural imitations the agents produce.

## Architecture and Implementation

Per the abstract, the architecture has three cooperating parts: an experience record in natural language, a reflection process over that record, and retrieval of relevant memories to plan behaviour. The deployment is a 25-agent sandbox world. Implementation detail beyond the abstract was not fetched.

## Code Examples

The source carries no reusable code on the abstract page.

## Best Practices

- Separate raw experience storage from synthesised reflection.
- Retrieve memory selectively for planning rather than replaying everything.
- Test each architectural component by ablation.

## Warnings and Anti-Patterns

- Dropping any of observation, planning or reflection reduces believability, per the ablation result.
- The evidence is from a simulated sandbox, not a production task setting.

## Related Concepts

- [[memory]]
- [[planning-and-reasoning]]
- [[reflexion]]
- [[what-is-an-ai-agent]]

## Future Work

The abstract does not state future work.

## References

- https://arxiv.org/abs/2304.03442
