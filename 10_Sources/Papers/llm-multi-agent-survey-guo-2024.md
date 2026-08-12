---
type: source
status: draft
created: 2026-08-13
title: "Large Language Model based Multi-Agents: A Survey of Progress and Challenges"
authors:
- Taicheng Guo
- Xiuying Chen
- Yaqi Wang
- Ruidi Chang
- Shichao Pei
- Nitesh V. Chawla
- Olaf Wiest
- Xiangliang Zhang
organisation: University of Notre Dame; King Abdullah University of Science and Technology; Southern University of Science and Technology; University of Massachusetts Boston
source_type: paper
venue: 
url: https://arxiv.org/abs/2402.01680
year: 2024
date_published: 
anthropic: false
topic:
- topic/research-papers
- topic/multi-agent
tags: [multi-agent, survey, agent-communication, agent-profiling, world-simulation]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
---

# Large Language Model based Multi-Agents: A Survey of Progress and Challenges

> Full citation: Taicheng Guo, Xiuying Chen, Yaqi Wang, Ruidi Chang, Shichao Pei, Nitesh V. Chawla, Olaf Wiest, and Xiangliang Zhang. "Large Language Model based Multi-Agents: A Survey of Progress and Challenges." arXiv:2402.01680v2, 2024. https://arxiv.org/abs/2402.01680

## Summary

This survey maps the field of LLM-based multi-agent systems, which the authors abbreviate to LLM-MA. Guo and co-authors argue that multi-agent systems gain two advantages over a single LLM agent: they specialise one model into distinct agents with different capabilities, and they let those agents interact to simulate complex environments. The survey dissects every reviewed system along four axes: the agents-environment interface, agent profiling, agent communication, and agent capability acquisition. It then sorts applications into two streams, problem solving and world simulation, and populates each with worked examples spanning software development, embodied robotics, science experiments, science debate, society, gaming, psychology, economy, recommender systems, policy making, and disease propagation. Section 5 catalogues three open-source frameworks, MetaGPT, CAMEL, and AutoGen, alongside the datasets and benchmarks each application domain uses. The paper closes with six challenges: multi-modal environments, hallucination that cascades between agents, collective intelligence, scaling the agent count, evaluation and benchmarks, and applications beyond the current set. The authors maintain an open-source GitHub repository to track new work.

## Key Concepts

- Two motivations separate a multi-agent system from a single agent: specialising one model into distinct profiles, and enabling interaction among those profiles.
- A four-part schema positions any LLM-MA system: agents-environment interface, agent profiling, agent communication, and agent capability acquisition.
- Applications split into two streams. Problem solving harnesses specialised expertise on a task. World simulation exploits role-playing to model a domain.
- Feedback drives capability. Agents learn from the environment, from other agents, from humans, or from nothing at all.
- Hallucination compounds in a multi-agent network. One agent's false output propagates to every agent that accepts it.
- Current systems adjust agents in isolation. That approach forfeits the synergy of coordinated multi-agent interaction.
- Scaling the agent count raises computational cost and makes agent orchestration a research problem in its own right.

## Terminology

- **LLM-MA** - the survey's abbreviation for an LLM-based multi-agent system.
- **Agents-environment interface** - the way agents perceive the environment, act on it, and learn from the outcome. Three types: sandbox, physical, and none.
- **Sandbox** - a simulated environment built by humans, such as a code interpreter or a set of game rules.
- **Physical** - a real-world environment where agents obey physics and produce direct physical outcomes.
- **Agent profiling** - the definition of an agent by its traits, actions, skills, and constraints. Three methods: pre-defined, model-generated, and data-derived.
- **Communication paradigm** - the style of interaction between agents: cooperative, debate, or competitive.
- **Shared message pool** - a communication structure from MetaGPT where agents publish messages and subscribe to the messages their profile matches.
- **Self-evolution** - an adjustment strategy where an agent modifies its own goals, planning strategies, or weights, rather than replaying stored history.
- **Dynamic generation** - the creation of new agents during system operation to meet a current need.
- **Agents orchestration** - the design of workflows, task assignments, and communication patterns across a large agent population.

## Architecture and Implementation

The survey specifies four axes for building or classifying an LLM-MA system. Section 3 sets out each axis with a table of worked examples.

**Agents-environment interface.** The environment defines the context a system runs in: software development, gaming, financial markets, or social behaviour modelling. Agents perceive the environment, act, and receive feedback that guides the next action. The Werewolf Game illustrates the loop. The sandbox sets day-night transitions, discussion periods, voting mechanics, and reward rules. Agents such as the werewolf and the Seer take role-specific actions, then read the resulting game state. Three interface types exist. Sandbox covers a simulated environment built by humans, with a code interpreter or a rule set standing in for the world. Physical covers real-world robotics, where an agent sweeps a floor or packs groceries, observes the result, and refines its action. None covers systems with no external environment, such as multi-agent debate, where the whole system is communication.

**Agent profiling.** Each agent carries a description of characteristics, capabilities, behaviours, and constraints tailored to a goal. A gaming system profiles players by role. A software system profiles a product manager and an engineer. A debating system profiles a proponent, an opponent, and a judge. Three profiling methods exist. Pre-defined profiles come from the system designer. Model-generated profiles come from an LLM. Data-derived profiles come from an existing dataset, such as MovieLens-1M for a recommender simulation. A system may combine two methods.

**Agent communication.** The survey splits communication into paradigm, structure, and content. The three paradigms are cooperative, where agents share a goal and exchange information towards a collective solution; debate, where agents argue, defend, and critique to converge on a refined answer; and competitive, where agent goals conflict. Four structures appear. Layered communication organises agents hierarchically, with each level holding distinct roles and interacting inside its layer or with adjacent layers. DyLAN, the Dynamic LLM-Agent Network, arranges agents in a multi-layered feed-forward network with inference-time agent selection and early stopping. Decentralised communication runs peer to peer, and dominates world simulation work. Centralised communication routes traffic through one coordinating agent or a small central group. The shared message pool comes from MetaGPT: agents publish to a common pool and subscribe by profile, which raises communication efficiency. Content takes the form of text in every reviewed system, and its substance follows the application. Software agents exchange code segments. Werewolf agents exchange suspicions and strategies.

**Agent capability acquisition.** Two elements govern how an agent improves: the feedback it receives, and the strategy it uses to adjust. Feedback arrives in text and comes from four sources. Environment feedback comes from a code interpreter or a simulator. Agent-interaction feedback comes from the judgement or the messages of other agents, as in science debate. Human feedback aligns the system with human values, and carries most weight in human-in-the-loop work. Some world simulations supply no feedback, because the study analyses the simulated result rather than agent planning. Three adjustment strategies follow. Memory stores prior interactions and feedback, then retrieves the entries that match the current goal. Self-evolution goes further: an agent alters its initial goals and planning strategies, or trains on feedback and communication logs. ProAgent anticipates teammate decisions and adjusts strategy from the communication log. Learning through Communication turns multi-agent logs into training data for fine-tuning. Dynamic generation creates new agents during operation, so the system scales to a need that appears at run time.

**Frameworks.** Section 5 compares three open-source implementations. MetaGPT encodes Standard Operating Procedures into prompts and assigns roles along an assembly line, which curbs hallucination on complex tasks. CAMEL uses inception prompting to steer two conversational agents towards autonomous cooperation, and doubles as a generator of conversational data. AutoGen offers customisation, letting a developer define agent interaction in both natural language and code.

**Benchmarks.** Table 2 lists the datasets each domain uses. Software development draws on HumanEval, MBPP, and SoftwareDev. Embodied AI draws on RoCoBench, C-WAH, TDW-MAT, and HM3D v0.2. Science debate draws on MMLU, MedQA, PubMedQA, GSM8K, StrategyQA, and Chess Move Validity. Society draws on SOTOPIA. Gaming draws on Werewolf, Avalon, Welfare Diplomacy, Overcooked-AI, Chameleon, and Undercover.

## Code Examples

The paper is a survey and contains no original code. It names three open-source frameworks a builder can adopt: MetaGPT, CAMEL, and AutoGen. The authors maintain a companion GitHub repository that tracks LLM-MA research.

## Best Practices

- Match the communication structure to the workflow. Software development follows a waterfall or an SOP sequence, so a layered structure fits.
- Use the shared message pool where communication volume is the bottleneck. Agents subscribe by profile and skip messages their role ignores.
- Encode human workflow insight into the system. MetaGPT converts Standard Operating Procedures into prompts for structured coordination.
- Put a human at the centre where an error costs money. Science experiment systems route agent output through human experts before action.
- Choose debate over cooperation where factual accuracy is the target. Multi-round debate improves factuality and inter-consistency across reasoning tasks.
- Combine profiling methods. Several reviewed systems pair pre-defined roles with model-generated or data-derived detail.
- Store feedback in memory and retrieve the entries that match the current goal, in preference to replaying the full history.

## Warnings and Anti-Patterns

- Do not treat single-agent hallucination controls as sufficient. Misinformation from one agent spreads through the network and compounds.
- Do not evaluate agents one at a time in a narrow scenario. That approach misses the emergent behaviour that defines a multi-agent system.
- Do not assume a benchmark exists for your domain. Science team operations, economic analysis, and disease propagation lack one.
- Do not add agents without a cost model. Each agent runs on a large model and demands compute and memory.
- Do not tune agents in isolation. Memory and self-evolution improve one agent and forfeit the collective intelligence of the network.
- Do not assign one LLM to every robot at scale. The context grows long and the cost becomes impractical.
- Do not expect an LLM agent to act as a rational game player. Agents overlook or revise refined beliefs when they act.
- Do not assume a text-only design transfers to sensory input. Multi-modal environments raise unsolved processing and grounding problems.

## Related Concepts

- [[supervisor-worker-multi-agent]]
- [[what-is-an-ai-agent]]
- [[memory]]
- [[planning-and-reasoning]]
- [[tool-use]]
- [[evaluation]]
- [[react]]
- [[reflexion]]
- [[agent-patterns-index]]
- [[workflow-vs-autonomous-agent]]
- [[10_Sources/Papers/autogen-wu-2023|AutoGen (Wu et al., 2023)]]
- [[10_Sources/Papers/camel-li-2023|CAMEL (Li et al., 2023)]]
- [[10_Sources/Papers/agentverse-chen-2023|AgentVerse (Chen et al., 2023)]]
- [[10_Sources/Papers/agent-architectures-landscape-masterman-2024|Agent Architectures Landscape (Masterman et al., 2024)]]

## Future Work

Section 6 sets out six challenges. Advancing into multi-modal environments asks how agents interpret images, audio, video, and physical action, since most work stops at text. Addressing hallucination asks how to detect and contain a false statement before other agents absorb it, which requires managing information flow as well as correcting one agent. Acquiring collective intelligence asks how to adjust many agents together, because current memory and self-evolution methods tune each agent alone and depend on a reliable interactive environment that resists design. Scaling up LLM-MA systems asks how to coordinate a large agent population under a compute budget, and names agents orchestration and the scaling laws of multi-agent behaviour as open problems. Evaluation and benchmarks asks for measures of emergent group behaviour, and for benchmarks in the domains that have none. Applications and beyond points to finance, education, healthcare, environmental science, and urban planning, and invites analysis through cognitive science, symbolic artificial intelligence, cybernetics, complex systems, and collective intelligence.

## References

- Canonical URL: https://arxiv.org/abs/2402.01680
- Hong et al., "MetaGPT," 2023.
- Li et al., "CAMEL: Communicative Agents," 2023.
- Wu et al., "AutoGen," 2023.
- Chen et al., "AgentVerse: Facilitating multi-agent collaboration and exploring emergent behaviors in agents," arXiv:2308.10848, 2023.
- Chen et al., "AutoAgents: A framework for automatic agent generation," arXiv:2309.17288, 2023.
- Chen et al., "Scalable multi-robot collaboration with large language models: Centralized or decentralized systems?" arXiv:2309.15943, 2023.
- Du et al., "Improving factuality and reasoning in language models through multi-agent debate," 2023.
- Xiong et al., "Examining inter-consistency of large language models," 2023.
- Chan et al., "ChatEval: Towards better LLM-based evaluators through multi-agent debate," 2023.
- Mandi et al., "RoCo: Multi-robot collaboration," 2023.
- Zhang et al., "CoELA: Cooperative Embodied Language Agent," 2023.
- Park et al., "Generative Agents," 2023.
- Park et al., "Social Simulacra," 2022.
- Gao et al., "S3: Social-network simulation system with large language model-empowered agents," arXiv:2307.14984, 2023.
- Zhang et al., "Agent4Rec," 2023.
- Hua et al., "WarAgent," 2023.
- Xiao et al., "Simulating public administration crisis," 2023.
- Williams et al., "Epidemic modelling with generative agents," 2023.
- Ghaffarzadegan et al., "Generative agent-based modeling," arXiv:2309.11456, 2023.
- Liu et al., "Dynamic LLM-Agent Network (DyLAN)," 2023.
- Nascimento et al., "Self-adaptive multi-agent systems," 2023.
- Zhang et al., "ProAgent," 2023.
- Wang et al., "Learning through Communication," 2023.
- Aher et al., "Turing Experiments," 2023.
- Dibia, "Multi-agent LLM applications: a review of current research, tools, and challenges," 2023.
