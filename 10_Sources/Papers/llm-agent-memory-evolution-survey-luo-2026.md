---
type: source
status: draft
created: 2026-08-13
title: "From Storage to Experience: A Survey on the Evolution of LLM Agent Memory Mechanisms"
authors:
- Jinghao Luo
- Yuchen Tian
- Chuxue Cao
- Ziyang Luo
- Hongzhan Lin
- Kaixin Li
- Chuyi Kong
- Ruichao Yang
- Jing Ma
organisation: Hong Kong Baptist University, South China Normal University, Hong Kong University of Science and Technology, National University of Singapore, University of Science and Technology Beijing
source_type: paper
venue: arXiv preprint
url: https://arxiv.org/abs/2605.06716
year: 2026
date_published: 2026-05
anthropic: false
topic:
- topic/research-papers
- topic/memory
tags: [memory, survey, agent-experience, continual-learning, trajectory-abstraction, self-evolution]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
af_targets:
- af:ADR-0005
- af:RSCH-04/Q11
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 8bdb1d72a142cf732a255ece7e80c25db6ed4b590883fda2321face0e7970083
---

# From Storage to Experience: A Survey on the Evolution of LLM Agent Memory Mechanisms

> Full citation: Jinghao Luo, Yuchen Tian, Chuxue Cao, Ziyang Luo, Hongzhan Lin, Kaixin Li, Chuyi Kong, Ruichao Yang, and Jing Ma. "From Storage to Experience: A Survey on the Evolution of LLM Agent Memory Mechanisms." arXiv, 2026. https://arxiv.org/abs/2605.06716

## Summary

This survey organises agent memory research as an evolution in three stages. Storage preserves interaction trajectories with minimal transformation. Reflection evaluates and corrects those trajectories. Experience abstracts clusters of trajectories into rules that transfer to unseen tasks. The axis of the taxonomy is the degree to which an agent uses its past trajectories. Substrate and module boundaries sit below that axis, not above it. The survey follows a Why-How-What structure across three research questions. Section 3 names three drivers of the evolution: long-range consistency, dynamic environments, and continual learning. Section 4 traces the path through the three stages and their sub-families. Section 5 isolates two frontier mechanisms of the Experience stage: active exploration and cross-trajectory abstraction. The authors argue that the field splits between operating-system engineering and cognitive science, and that the split hides the technical drivers of progress. The survey states its own limits: it offers no quantitative comparison, since no single benchmark spans all three stages.

This paper differs from [[10_Sources/Papers/llm-agent-memory-survey-du-2026|Du's memory survey]] in its organising axis. Du classifies a memory design along three independent dimensions: temporal scope, representational substrate, and control policy. A design occupies a point in that space at one moment. Luo instead builds a developmental sequence, where each stage consumes the output of the stage before it. Du devotes a large share of its length to benchmarks, to the recall-versus-decision gap, and to production engineering guidance. Luo devotes its weight to the Experience stage, which Du treats as one mechanism family among five. The two surveys share source material on MemGPT, Reflexion, and Generative Agents, and diverge on what that material demonstrates.

## Key Concepts

- Memory evolves along the depth of trajectory use, from faithful recording to error correction to cross-trajectory abstraction.
- The three stages do not replace one another. A mechanism retains traits of the earlier stage while its essence moves to the next.
- Reflection transforms a single trajectory. Experience induces over a batch of trajectories. That distinction carries the survey.
- Memory is an externalised repository that bridges the frozen parametric knowledge of the model and the changing dynamics of the environment.
- Long-range consistency splits into state consistency and goal consistency. Both push agents toward persistent memory modules.
- Stale knowledge fails without warning: an outdated record stays close in embedding space while its content has lost validity.
- Unbounded memory growth harms performance, because errors propagate through the store and contaminate later learning.
- Agents show a bias toward following past successful trajectories, so a corrected trajectory without abstraction still misfires under a context shift.
- Active exploration and cross-trajectory abstraction form a feedback loop. Prior experience aims the exploration; exploration outcomes feed the abstraction.

## Terminology

- **Trajectory** - a chronological sequence of observation-action pairs within one task session, written as tau.
- **Storage** - the stage that holds a one-to-one correspondence between memory entries and execution traces.
- **Reflection** - a semantic transformation from a trajectory to an evaluated or corrected reasoning path, conditioned on evaluation criteria.
- **Experience** - an inductive operator over a batch of similar trajectories that returns a set of general rules.
- **Policy prior** - the rule set produced by the Experience stage, which lifts the agent policy above rule-consistent action.
- **Minimum Description Length principle** - the compression target the Experience stage adopts when it folds redundant trajectories into schemas.
- **Active exploration** - memory-guided pursuit of new experience, driven by reward, curriculum, or reuse of past trajectories.
- **Cross-trajectory abstraction** - induction across trajectory groups by contrast, distillation, code encapsulation, or gradient internalisation.
- **Latent modulation** - encoding experience as latent variables injected into current reasoning, with no parameter update.
- **Parameter internalisation** - folding explicit trajectories into model weights through gradient updates.
- **Hybrid experience** - an accumulate-and-internalise cycle that treats the explicit store as a cache for periodic weight updates.

## Architecture and Implementation

The survey formalises the agent before it formalises memory. An agent is a decision entity with parameters theta, acting in a dynamic environment E under a policy that maps context to a distribution over the action space. At step t the agent receives an observation and retrieves context-specific memory from the global repository. The action is sampled given the static system instruction, the observation, and the retrieved memory. The survey separates the global repository M from its retrieved instantiation at time t. That separation is what lets the three stages differ: each stage changes what M holds and what retrieval returns, without changing the agent loop around it.

**Storage.** The raw store accumulates trajectories as a set. Storage designs split into three families. Linear storage treats the record as a token stream under a first-in, first-out policy. Its two branches are context window adaptation, which reworks attention, positional encoding, or input structure to widen the usable input, and information sparsification, which drops low-utility tokens by attention score, query-key similarity, or perplexity. Neither branch alters the semantics of what it stores. Vector storage encodes trajectories into a high-dimensional space and shifts the design problem from storage to retrieval. Semantic retrieval ranks by geometric proximity in embedding space. Weighted retrieval adds scoring signals: MemoryBank models temporal decay with the Ebbinghaus forgetting curve, and the Stanford Town agents combine relevance, recency, and importance. Structured storage imposes explicit relations. Its three branches are tabular databases, which hold agent knowledge in relational form and translate natural language to SQL through a controller; tiered architectures, where MemGPT separates main context from external context to give virtual context expansion; and semantic graphs, which model interaction history as entities and relations for multi-hop retrieval and precise update.

**Reflection.** Storage leaves memory quality untouched, since raw trajectories carry hallucinations, logic errors, and dead attempts. Reflection maps a completed trajectory to a refined memory unit under evaluation criteria, then injects that unit back into the repository. The refined unit becomes an independent entry, decoupled from the noise of the original trajectory. Three feedback sources organise the stage. Introspection uses the model's own knowledge and runs through three pathways: error rectification, where Reflexion distils corrective feedback from failed trajectories into textual memory; dynamic maintenance, which manages the memory lifecycle through clustering, entity-relation updates, and operating-system-style controllers; and knowledge compression, which folds long trajectories into modular procedural memories or folded contexts. Environmental reflection anchors the process in outcomes from the world. It splits into environment modelling, which infers world rules from demonstrations and summarises tool behaviour from execution outcomes, and decision optimisation, which treats memory management as a learnable policy under outcome-based rewards. Coordination extends reflection to a society of agents through role division and consensus, with heterogeneous modules for core, episodic, and semantic memory.

**Experience.** Reflected memories stay fragmented and context-bound, which raises retrieval cost and inference burden on new tasks. The Experience function takes a subset of trajectories similar in topology and returns a rule set that serves as a policy prior. Table 1 of the paper sets out the contrast. Reflection performs intra-trajectory transformation and yields a unit tied to the original task context, retrieved to assist past tasks of similar meaning. Experience performs inter-trajectory induction and yields rules detached from any scenario, applicable without trajectory-level matching. The survey names Reflexion, CLIN, and AgentFold as reflection work, and FLEX, MemSkill, and SkillRL as experience work. Implementation splits three ways. Explicit experience produces human-readable artefacts: heuristic guidelines as natural language rules, experience graphs that capture logical dependency, and procedural primitives that encapsulate high-frequency action sequences into callable functions. A further line distils trajectories into an evolvable skill library with a lifecycle of induction, reuse, and refinement. Implicit experience removes the retrieval step. Latent modulation generates and injects latent token sequences conditioned on the current reasoning state, as in MemGen's Memory Weaver, or alternates fast retrieval with slow integration in latent space. Parameter internalisation writes experience into weights through distillation of corrective hints, through experience stripping that removes retrieval segments during training, or through reinforcement learning over agent trajectories. Hybrid experience runs an accumulate-and-internalise cycle, treating the explicit pool as a high-capacity cache that periodic parameter updates absorb. That cycle targets storage explosion and retrieval latency at once.

**Frontier mechanisms.** Active exploration turns the agent from a recorder into a collector of experience under goals. Its drivers are reward signals, curricula of rising difficulty, and reuse of abstracted history. Its dimensions are breadth, which attacks knowledge gaps in unfamiliar environments through curiosity; depth, which extracts high-order skills inside a vertical task; and strategy, which optimises decision paths over long horizons. Cross-trajectory abstraction supplies four mechanisms: contrastive induction over success and failure pairs, distillation of fine-grained actions into higher-order thought patterns, code encapsulation of recurring behaviour, and gradient internalisation of trajectory groups. Its granularity runs three levels. Shallow abstraction keeps semantic logic as natural language rules. Intermediate abstraction strips the language and keeps a modular execution skeleton. Deep abstraction compresses the trajectory distribution into weights and turns experience into decision intuition.

## Code Examples

The survey carries no code. It maintains a public list of papers and resources at https://github.com/FeishuLuo/Evolving-LLM-Agent-Memory-Survey, and it names systems that expose the mechanisms in implementable form: MemGPT for tiered context, Mem0 and Zep for lifecycle maintenance, and MemGen for latent injection.

## Best Practices

- Choose the memory stage from the task demand. A single-session task needs faithful storage; an open-world task that recurs needs abstraction.
- Anchor reflection in environmental outcomes where the task allows it, since introspection alone risks drift from fact.
- Bound the store. Strategic addition and deletion beat unlimited accumulation, because scale carries error with it.
- Attach temporal awareness, decay policies, and flexible retrieval to any long-lived store, since correct strategies lose utility as the world moves.
- Separate the refined memory unit from the rule set. One assists a similar past task; the other primes an unseen scenario.
- Prefer explicit experience where the team needs interpretation and hand editing, and implicit experience where inference overhead dominates.
- Model causal dependency across time steps rather than the record of interactions alone, since real environments carry delayed and cascading effects.

## Warnings and Anti-Patterns

- Do not treat memory expansion as progress. Unrestricted growth propagates errors through the store and degrades learning.
- Do not trust semantic similarity as a validity check. An outdated record stays close in embedding space while its content has expired.
- Do not stop at reflection. A corrected trajectory without abstraction still triggers errors under a small context shift, because agents follow past success paths.
- Do not retrieve without a gate. Indiscriminate retrieval of irrelevant or obsolete memories breaks reasoning coherence.
- Do not read the label "experience" as the concept the survey defines. Parts of the literature use the term for work outside that scope.
- Do not compare mechanisms across stages by number. The stages hold different design objectives, and no unified benchmark covers them.
- Do not textualise every modality. Conversion to text loses information that resists articulation in words.

## Related Concepts

- [[memory]]
- [[reflexion]]
- [[the-agent-loop]]
- [[planning-and-reasoning]]
- [[retrieval-augmented-generation]]
- [[knowledge-graph]]
- [[10_Sources/Papers/llm-agent-memory-survey-du-2026|Memory for Autonomous LLM Agents]]
- [[10_Sources/Papers/reflexion-shinn-2023|Reflexion]]
- [[10_Sources/Papers/vizomem-liang-2026|VizoMem]]

## Future Work

The survey sets out five directions. Active memory perception asks memory to judge whether a task needs recall at all, and which type, in place of passive triggering and blanket retrieval. Organisation of working memory treats the in-task buffer as the next bottleneck, and points to interval isolation, retrospective integration of decision nodes, and adaptive pruning. Benchmarks for experience address a gap the survey documents in its dataset appendix: existing datasets test retrieval and denoising, while abstraction and generalisation go untested. Four of the benchmarks tabulated sit in the Experience stage, against 14 in Storage and 15 in Reflection. Distributed shared memory targets multi-agent organisations, where current sharing runs through explicit dialogue and hits bandwidth limits and exchange noise; the survey calls for consensus memory systems instead. Multimodal memory asks for units with unified temporality and semantics across vision, audio, and text. The appendix records that multimodal work concentrates in the Storage stage, with scarce coverage of Reflection and Experience, and it names three obstacles: alignment across asymmetric signal granularity, temporal consistency where event boundaries defy physical time, and consolidation where no single metric measures similarity across modalities.

## References

- Canonical URL: https://arxiv.org/abs/2605.06716
- Resource list: https://github.com/FeishuLuo/Evolving-LLM-Agent-Memory-Survey
- Yao et al., "ReAct: Synergizing reasoning and acting in language models," arXiv:2210.03629, 2022.
- Shinn et al., "Reflexion: Language agents with verbal reinforcement learning," 2023.
- Packer et al., "MemGPT," 2023.
- Park et al., "Generative Agents," 2023.
- Zhong et al., "MemoryBank," 2023.
- Hu et al., "ChatDB: Augmenting LLMs with databases as their symbolic memory," arXiv:2306.03901, 2023.
- Majumder et al., "CLIN," 2023.
- Anokhin et al., "AriGraph," 2024.
- Chhikara et al., "Mem0," 2025.
- Rasmussen et al., "Zep," 2025.
- Cai et al., "FLEX," 2025.
- Zhang et al., "MemGen," 2025.
- Zhang et al., "LatentEvolve," 2025.
- Ouyang et al., "ReasoningBank," 2025.
- Wu et al., "EvolveR," 2025.
- Ye et al., "AgentFold," 2025.
- Du et al., "Rethinking memory in AI: Taxonomy, operations, topics, and future directions," arXiv:2505.00675, 2025.
- Wu et al., "StreamBench," 2024.
- Ai et al., "MemoryBench," arXiv:2510.17281, 2025.
- Wei et al., "Evo-Memory," 2025.
- Zheng et al., "LABench," 2025.
