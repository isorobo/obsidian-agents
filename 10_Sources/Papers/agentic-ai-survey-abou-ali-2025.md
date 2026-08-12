---
type: source
status: draft
created: 2026-08-13
title: "Agentic AI: a comprehensive survey of architectures, applications, and future directions"
authors:
- Mohamad Abou Ali
- Fadi Dornaika
- Jinan Charafeddine
organisation: University of the Basque Country (UPV/EHU); Lebanese International University; De Vinci Higher Education
source_type: paper
venue: Artificial Intelligence Review
url: https://doi.org/10.1007/s10462-025-11422-4
year: 2025
date_published: 2025-11-14
anthropic: false
topic:
- topic/research-papers
- topic/architectures
tags: [agentic-ai, survey, neuro-symbolic, multi-agent, ai-governance, prisma-review]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
---

# Agentic AI: a comprehensive survey of architectures, applications, and future directions

> Full citation: Mohamad Abou Ali, Fadi Dornaika and Jinan Charafeddine. "Agentic AI: a comprehensive survey of architectures, applications, and future directions." Artificial Intelligence Review (2026) 59:11. Received 20 July 2025, accepted 7 October 2025, published online 14 November 2025. Open access under CC BY 4.0. https://doi.org/10.1007/s10462-025-11422-4

## Summary

This survey splits Agentic AI into two lineages and reads the literature through that split. The authors name the field's central error conceptual retrofitting. It describes modern LLM-driven agents in symbolic vocabulary, such as belief-desire-intention (BDI) and the perceive-plan-act-reflect (PPAR) loop. Their dual-paradigm framework separates the symbolic/classical lineage, which rests on algorithmic planning and persistent state, from the neural/generative lineage, which rests on stochastic generation and prompt-driven orchestration. The method is a PRISMA 2020 review across IEEE Xplore, ACM Digital Library, arXiv, SpringerLink, ScienceDirect, and Google Scholar, covering January 2018 to March 2025. Screening reduced 165 records to 78 eligible studies; 12 seminal symbolic papers were added for historical context, giving a corpus of 90. Two coders applied the scheme in NVivo and reached a Cohen's Kappa of 0.82. Three findings dominate. Paradigm choice tracks the domain: symbolic and hybrid systems hold safety-critical work such as healthcare and robotics, while neural systems hold data-rich work such as finance and education. Governance research crowds around neural risks and leaves symbolic systems underserved. Research shifted from symbolic and hybrid cognitive architectures (2018 to 2021) to neural orchestration frameworks after 2022. The authors set out nine research gaps, six ethical challenge areas, and a roadmap that ends in neuro-symbolic integration rather than the victory of one lineage.

## Key Concepts

- Conceptual retrofitting: the misapplication of BDI, SOAR, and PPAR vocabulary to LLM-orchestrated systems, which creates a false sense of continuity between incompatible architectures.
- The dual-paradigm taxonomy: symbolic/classical systems act through algorithmic planning over explicit state; neural/generative systems act through stochastic generation over a prompt-managed context.
- An AI Agent is one autonomous system that finishes a goal alone; Agentic AI is the broader approach that orchestrates teams of specialised agents.
- Paradigm-market fit: domain constraints of ethics, regulation, and epistemics decide the paradigm, not technical superiority.
- The governance imbalance: ethics research concentrates on neural risks, so complex symbolic systems in safety-critical deployments carry an unexamined burden.
- Coordination separates the lineages: symbolic agents negotiate through engineered protocols; neural agents coordinate through structured conversation.
- Evaluation must follow the paradigm: symbolic systems answer to verifiability, neural systems answer to robust adaptability.
- The attribution gap: stochastic, emergent behaviour breaks legal frameworks built on direct causation and intent.

## Terminology

- **Conceptual retrofitting**: description of a neural agentic system in the language of a symbolic one, which hides its true mechanics.
- **Symbolic/classical lineage**: the paradigm of explicit logic, algorithmic planning, and deterministic or probabilistic models.
- **Neural/generative lineage**: the paradigm where agency emerges from prompt-driven orchestration of generative models.
- **PPAR loop**: the perceive-plan-act-reflect cycle that symbolic cognitive architectures implement over symbolic representations.
- **MDP**: a model of a fully observed environment as the tuple (S, A, P, R) of states, actions, transition probabilities, and rewards.
- **POMDP**: an extension of the MDP that carries probabilistic belief states for environments with incomplete information.
- **BDI and SOAR**: cognitive architectures that map belief, desire, intention, and meta-cognition onto working memory, motivation, executive control, and self-monitoring.
- **LLM orchestration**: the architectural shift from designing a cognitive agent to coordinating a generative pipeline.
- **Contract net protocol (CNP)**: a symbolic negotiation protocol where a manager agent calls for proposals and awards a task to the best bidder.
- **Blackboard system**: a shared memory space where specialist agents contribute to a solution as relevant data appears.
- **Perverse instantiation**: a symbolic failure where an agent executes a flawed goal specification to the letter, with damaging results.
- **Goal completion fidelity**: the share of pre-defined subgoals a symbolic plan achieves.
- **Plan optimality**: the cost of an agent's plan measured against a known optimal solution.

## Architecture and Implementation

The survey builds its architecture account from the two lineages down to named frameworks. Five historical eras set the stage: symbolic AI (1950s to 1980s), machine learning (1980s to 2010s), deep learning (2010s to present), generative AI (2014 to present), and Agentic AI (2022 to present). The transformer of 2017 is the pivot. It produced the LLM substrate that made the neural paradigm feasible.

The symbolic lineage stacks three layers. MDPs model fully observed environments through states, actions, transition probabilities, and rewards, and they suit deterministic rule-based domains. POMDPs add belief states so an agent can infer hidden state from observation, at the cost of belief-tracking overhead that limits scale. Cognitive architectures such as BDI and SOAR sit at the top and implement a PPAR loop over symbolic representations. Table 2 maps the modules to human functions: the belief module to working memory and a symbolic knowledge base, the desire module to motivation and a goal stack or utility function, the intention module to executive control and an action policy or planner, and the meta-cognition layer to self-reflection and a monitor-replan loop. The authors call these systems powerful, brittle, and hard to scale.

The neural lineage starts with deep reinforcement learning. DRL learns policies from high-dimensional input, and proximal policy optimisation (PPO) stabilises that learning. Meta-DRL adds a second optimisation loop for generalisation across tasks, which the authors treat as a precursor to modern adaptability. The LLM then breaks the line rather than extending it. Agency becomes a property of prompt-driven orchestration, and the design task becomes pipeline construction.

Table 7 classifies five production frameworks by orchestration mechanism and by the symbolic function each one displaces. LangChain uses prompt chaining and orchestrates linear sequences of LLM calls and API tools, replacing symbolic planning. AutoGen uses multi-agent conversation and structures dialogue between collaborating agents, replacing monolithic control. CrewAI assigns roles and goals to a team and manages the interaction workflow, replacing the centralised scheduler. Semantic Kernel composes plugins and functions, connecting the model to pre-written code "skills" and replacing integrated actuation. LlamaIndex supplies data connectors, indexing, and retrieval-augmented generation, replacing the internal symbolic knowledge base with external context retrieval.

Multi-agent orchestration is the top of the neural paradigm. A central orchestrator, often an LLM, acts as context manager and task router. It reads the goal and assigns subtasks to specialised agents through structured messaging. Capability comes from the quality of the orchestration, not from the cognitive depth of any one agent.

Coordination protocols divide the lineages further, and Table 8 compares them across six features. Symbolic coordination runs on the contract net protocol, blackboard systems, and market-based resource allocation, with JADE, JaCaMo, and early SOAR systems as the named platforms. State is explicit and centralised, decisions follow rules, flexibility is low, and the protocol admits formal verification. Neural coordination runs on conversation-based group chat (AutoGen), role-based workflow (CrewAI), and dynamic context management through state machines (LangGraph). State sits inside the context window, the next action comes from stochastic generation, flexibility is high, and the executed path resists tracing. The authors summarise the trade as verifiable reliability against adaptable emergence.

Domain implementations show the trade in practice. Healthcare keeps rule-based clinical decision support for auditable tasks and wraps neural components, such as structured report generation and on-premise edge agents, inside deterministic tool-chaining pipelines. Finance runs CrewAI role-based workflows for market analysis because the role trail supports audit, and grounds sentiment models in retrieved data through RAG to cut hallucination; symbolic systems hold high-frequency trading and core regulatory logic. Robotics stays hybrid, pairing POMDP planners for safety with neural components for adaptability. Legal and compliance work appears as neural agents bounded by symbolic retrieval. Scientific research uses AutoGen for exploratory multi-agent discussion, while symbolic systems keep theorem proving and deductive inference.

## Code Examples

The paper is a survey and carries no code. It names frameworks and their orchestration mechanisms as the reusable artefact: LangChain, AutoGen, CrewAI, Semantic Kernel, LlamaIndex, and LangGraph on the neural side; JADE, JaCaMo, and SOAR on the symbolic side.

## Best Practices

- Classify a system by its operational mechanism before you describe it, so the vocabulary matches the architecture.
- Choose the paradigm from the domain constraint. Safety, auditability, and regulation favour symbolic or constrained hybrid designs; unstructured data and adaptation favour neural designs.
- Contain a neural component inside a deterministic tool-chaining pipeline where the setting demands reliability, as clinical deployments do.
- Ground stochastic output in verified data through retrieval-augmented generation to reduce hallucination in finance and legal work.
- Evaluate a symbolic system on goal completion fidelity, plan optimality, logical soundness under formal methods, and edge case handling.
- Evaluate a neural system on long-horizon task success, context and memory management, tool use proficiency, prompt robustness including injection resilience, and cost and latency.
- Combine automated metrics, human judgement of output quality, and adversarial red teaming rather than trusting one signal.
- Run agents in sandboxed testing environments. The paper marks this as the one mitigation that applies to both paradigms.
- Match human oversight to the paradigm: explicit veto points and interrupt signals for symbolic agents, confidence thresholds and context steering for neural agents.

## Warnings and Anti-Patterns

- Do not retrofit symbolic concepts onto LLM systems. Mapping AutoGen or CrewAI to PPAR or BDI hides the prompt-driven mechanics that make them work.
- Do not measure agency with accuracy. Accuracy misses autonomy, task success, efficiency, and robustness.
- Do not write architecture-agnostic governance. A "full explainability" requirement suits a symbolic system and stays out of reach for a pure neural agent.
- Do not assume the audit trail exists. Neural coordination paths stay opaque, and post-hoc explanations prove unreliable.
- Do not leave symbolic governance unbuilt. Symbolic AI holds the safety-critical deployments where the governance gap bites hardest.
- Do not expect a hybrid system to inherit the easier half. A neuro-symbolic agent inherits the audit burden of the symbolic side and the monitoring burden of the neural side.
- Do not treat AgentBench and GAIA as sufficient. The authors report that both miss subtle misalignment, prompt robustness, and the true cost of context management.
- Do not build an opaque oracle. Conversational interfaces invite over-trust when the user cannot steer or interpret the output.
- Do not assume tool access equals tool understanding. Neural agents call APIs well and misuse them when semantic understanding of the tool fails.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[agent-vs-llm]]
- [[workflow-vs-autonomous-agent]]
- [[supervisor-worker-multi-agent]]
- [[planning-and-reasoning]]
- [[the-agent-loop]]
- [[tool-use]]
- [[memory]]
- [[retrieval-augmented-generation]]
- [[evaluation]]
- [[agent-patterns-index]]
- [[10_Sources/Papers/agent-architectures-landscape-masterman-2024|Agent architectures landscape (Masterman 2024)]]
- [[10_Sources/Papers/llm-autonomous-agents-survey-wang-2025|LLM autonomous agents survey (Wang 2025)]]
- [[10_Sources/Papers/llm-multi-agent-survey-guo-2024|LLM multi-agent survey (Guo 2024)]]
- [[10_Sources/Papers/ai-agent-systems-survey-xu-2026|AI agent systems survey (Xu 2026)]]

## Future Work

Table 9 sets out nine gap areas, each split by paradigm. Evaluation and benchmarks need paradigm-specific suites: logical soundness and failure predictability for symbolic systems, hallucination under pressure, prompt injection resilience, and multi-session consistency for neural systems. Reasoning and adaptability needs neuro-symbolic research, where neural parts handle pattern recognition and symbolic modules enforce constraint checking. Long-term autonomy and memory needs efficient belief revision on the symbolic side and external structured memory that agents read and write on the neural side. Infrastructure dependence calls for energy-efficient and decentralised compute, model distillation, sparse architectures, and hybrid cloud-edge deployment. Human-AI interaction needs logic and state visualisation for symbolic agents, and context steering, confidence communication, and collaborative task management for neural agents. Trust and transparency needs explicable goal structures on one side and mechanistic interpretability with faithful real-time explanation on the other. Safety and alignment needs formal verification of goals and constraints for symbolic systems, and red teaming, adversarial training, and constitutional oversight for neural systems. Interoperability needs paradigm bridging: APIs that let a neural agent query a symbolic reasoner for validation, and let a symbolic system call a neural network for perception. Governance and accountability needs decision-logic audit trails for symbolic systems, and mandatory context logging, output watermarking, and new forms of developer liability for neural systems.

Table 10 turns the gaps into strategic trajectories across multi-agent ecosystems, technological convergence, self-evolving architectures, human-AI collaboration, governance-first design, scientific discovery, and research priorities. Four themes carry the roadmap. Neuro-symbolic integration is the keystone. Future ecosystems will hold specialised agents of both kinds behind standardised protocols, and orchestrating those hybrid swarms is a research frontier. Governance runs on two tracks, formal methods for symbolic verifiability and statistical methods for neural alignment, and a hybrid agent needs both. Convergence with IoT, robotics, blockchain, and quantum computing amplifies both paradigms.

The authors state four limits on their own work. Temporal dynamics leave recent developments uncaptured despite a search reaching early 2025. Proprietary neural systems restrict access to architectural detail and performance data. Heterogeneous evaluation metrics block direct cross-paradigm benchmarking. Assigning hybrid architectures to a single paradigm forced simplification in some cases.

## References

- Canonical URL: https://doi.org/10.1007/s10462-025-11422-4
- Kaelbling et al. (1998), foundational work on MDPs and POMDPs.
- Laird (2022), the SOAR cognitive architecture.
- Wu et al. (2023), AutoGen.
- Venkadesh et al. (2024) and Duan and Wang (2024), CrewAI and LangGraph.
- Mavroudis (2024), LangChain.
- Gheorghiu (2024), LlamaIndex and RAG.
- Kothapalli (2024), Semantic Kernel.
- Liu et al. (2023), AgentBench.
- Mialon et al. (2023), GAIA.
- Xu and Weigand (2001), the contract net protocol.
- Craig (1988), blackboard systems.
- Page et al. (2021a, b), PRISMA 2020.
- Thomas and Harden (2008), thematic synthesis.
- Masterman et al. (2024), the landscape of emerging AI agent architectures.
- Gabison and Xian (2025), liability in LLM-based agentic systems.
- Chan et al. (2023, 2024), harms from agentic systems and visibility into AI agents.
