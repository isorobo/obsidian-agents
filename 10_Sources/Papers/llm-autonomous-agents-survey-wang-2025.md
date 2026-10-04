---
type: source
status: draft
created: 2026-08-13
title: "A Survey on Large Language Model based Autonomous Agents"
authors:
- Lei Wang
- Chen Ma
- Xueyang Feng
- Zeyu Zhang
- Hao Yang
- Jingsen Zhang
- Zhi-Yuan Chen
- Jiakai Tang
- Xu Chen
- Yankai Lin
- Wayne Xin Zhao
- Zhewei Wei
- Ji-Rong Wen
organisation: Gaoling School of Artificial Intelligence, Renmin University of China
source_type: paper
venue: Frontiers of Computer Science
url: https://doi.org/10.1007/s11704-024-40231-1
year: 2025
date_published: 
anthropic: false
topic:
- topic/research-papers
- topic/architectures
tags: [survey, agent-architecture, unified-framework, capability-acquisition, evaluation]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
af_targets:
- af:RSCH-04/Q01
- af:RSCH-04/Q30
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: fd1c9c1a647a6e0c618c5bac545141fad7c0d651b70894a85f67bbddc216468b
---

# A Survey on Large Language Model based Autonomous Agents

> Full citation: Lei Wang, Chen Ma, Xueyang Feng, Zeyu Zhang, Hao Yang, Jingsen Zhang, Zhi-Yuan Chen, Jiakai Tang, Xu Chen, Yankai Lin, Wayne Xin Zhao, Zhewei Wei, and Ji-Rong Wen. "A Survey on Large Language Model based Autonomous Agents." Frontiers of Computer Science, 2025, pages 1 to 42. https://doi.org/10.1007/s11704-024-40231-1

## Summary

Wang and colleagues review the field of autonomous agents built on large language models. The survey organises the field around three questions: how to construct an agent, where to apply it, and how to evaluate it. Construction splits into two halves. Architecture design supplies the hardware; the paper proposes a unified framework of four modules covering profile, memory, planning, and action. Capability acquisition supplies the software, and the paper sorts methods by whether they fine-tune the LLM. It names a third route beyond fine-tuning and prompt engineering: mechanism engineering. Applications span social science, natural science, and engineering, from psychology simulation and jurisprudence to chemistry assistants and robotics. Evaluation divides into subjective strategies, meaning human annotation and the Turing test, and objective strategies built from metrics, protocols, and benchmarks. The authors compile 100 works, map each to their taxonomy in three tables, and close with six open challenges. The paper positions itself as the first survey scoped to LLM-based agents rather than to LLMs at large.

## Key Concepts

- A unified four-module framework covers most prior agent work: profile, memory, planning, and action. The profile module shapes memory and planning; those three modules together drive the action module.
- Architecture design maps to defining a network structure, while capability acquisition maps to learning its parameters. Architecture alone leaves the agent without task-specific skill.
- LLM-based agents hold broader internal world knowledge than reinforcement learning agents, so they act without training on domain data. They also expose a natural language interface, which raises flexibility and explainability.
- Memory structures divide into unified memory, which simulates short-term memory alone, and hybrid memory, which models short-term and long-term memory together. Long-term-only memory is absent from the literature, since consecutive agent actions correlate.
- Planning divides on one axis: whether the agent receives feedback after acting. Planning without feedback suits short reasoning chains; planning with feedback handles long-horizon tasks.
- Mechanism engineering is a capability route unique to agents. It develops specialised modules and working rules rather than adjusting parameters or prompts.
- Subjective and objective evaluation each carry weaknesses, so the authors argue for combining them.

## Terminology

- **Profiling module**: the component that fixes the agent role, written into the prompt as demographic, psychological, and social information.
- **Handcrafting method**: manual specification of agent profiles. Flexible, and costly at scale.
- **LLM-generation method**: automatic profile generation from rules plus seed profiles. Cheap, and loose on control.
- **Dataset alignment method**: profiles drawn from real-world datasets such as the American National Election Studies.
- **Unified memory**: short-term memory realised through in-context learning, written into the prompt.
- **Hybrid memory**: short-term buffering of recent perception plus long-term consolidation, often in a vector store.
- **Memory reflection**: the operation that summarises stored low-level records into abstract, high-level insight.
- **Single-path reasoning**: task decomposition into a cascade where each step leads to one successor.
- **Multi-path reasoning**: task decomposition into a tree or graph where each step admits several successors.
- **External planner**: a purpose-built solver, such as a PDDL planner, that the LLM feeds and reads back from.
- **Action space**: the set of available actions, drawn from external tools or from the internal knowledge of the LLM.
- **Mechanism engineering**: capability acquisition through trial-and-error loops, crowd-sourcing, experience accumulation, and self-driven evolution.
- **Hyper-accuracy distortion**: the tendency of models such as GPT-4 to return estimates too perfect for a human simulation.

## Architecture and Implementation

The unified framework composes four modules. The profiling module identifies the role. The memory and planning modules place the agent in a dynamic environment, so it recalls past behaviour and plans future behaviour. The action module translates decisions into outputs. Influence runs one way: profile shapes memory and planning, and all three shape action.

### Profiling module

Profiles carry basic information such as age, gender, and career, psychological information reflecting personality, and social information describing relationships between agents. The application scenario decides which matters. Three generation strategies exist. Handcrafting assigns profiles by hand, as in Generative Agents, MetaGPT, and ChatDev, where roles and responsibilities are predefined for software development. LLM-generation seeds a few profiles by hand, then prompts a model to produce the rest, as RecAgent does. Dataset alignment converts records about real people into natural language prompts. The authors argue for combining strategies: profile part of a population from real data, then hand-assign roles that do not yet exist to forecast social change.

### Memory module

Memory design borrows from cognitive science, mapping short-term memory to the transformer context window and long-term memory to external vector storage. Unified memory writes state into the prompt each round. RLP maintains speaker and listener states, SayPlan uses scene graphs and environment feedback, and DEPS treats generated task plans as short-term memory. The context window bounds this design. Hybrid memory answers that bound. Generative Agents hold current context in short-term memory and past behaviour in long-term memory, retrieved against current events. AgentSims encodes daily memories as embeddings in a vector database. GITM stores the current trajectory short-term and reference plans summarised from successful trajectories long-term. Reflexion pairs a short-term sliding window over recent feedback with persistent condensed insight.

Formats vary along a second axis. Natural language keeps memory flexible and semantically rich, as in Reflexion and Voyager. Embeddings raise retrieval efficiency, as in MemoryBank's dual-tower dense retrieval. Databases give precise manipulation, as in ChatDB, where the agent issues SQL to add, delete, and modify records. Structured lists carry semantics in compact form, as in GITM's hierarchical action tree and RET-LLM's triplet phrases. Formats combine. GITM uses a key-value list where keys are embedding vectors and values are raw natural language, which buys retrieval speed and comprehension together.

Three operations connect memory to the environment. Memory reading extracts records by a weighted score over recency, relevance, and importance, where importance depends on the record alone and not on the query. Balancing parameters recover the strategies in the literature: zero weight on recency and importance reduces reading to relevance alone, which several systems use, while equal weights across all three reproduce the Generative Agents design. Memory writing faces two problems. Duplication is handled by condensing a list of similar sequences into one plan once it reaches five entries, or by count accumulation as in Augmented LLM. Overflow is handled by user-commanded deletion in ChatDB or a first-in-first-out buffer in RET-LLM. Memory reflection summarises stored records into insight. In Generative Agents the agent poses three questions from recent memory, queries memory with them, then generates five insights. Reflection nests, so insights build on insights. ExpeL reflects by comparing successful against failed trajectories on the same task.

### Planning module

Planning without feedback comes in three forms. Single-path reasoning cascades steps: Chain of Thought supplies reasoning steps as prompt examples, Zero-shot-CoT triggers them with "think step by step", RePrompting checks preconditions before each step and regenerates on failure, ReWOO separates plans from observations then combines them, and HuggingGPT decomposes a task into sub-goals solved through Hugging Face models. SWIFTSAGE splits fast pattern response from deep planning under dual-process theory. Multi-path reasoning branches: CoT-SC samples several reasoning paths and takes the majority answer, Tree of Thoughts searches a tree of intermediate thoughts by breadth-first or depth-first search under LLM evaluation, GoT generalises that tree to a graph, and RAP builds a world model and aggregates Monte Carlo tree search iterations. External planners take a third route. LLM+P converts the task into PDDL, solves it with a classical planner, and converts the result back. CO-LLM shows LLMs plan well at high level and control poorly at low level, so it delegates low-level execution to a heuristic planner.

Planning with feedback handles long horizons, where a flawless initial plan is out of reach and transition dynamics break execution. Environmental feedback drives ReAct, which builds prompts from thought, act, and observation triplets so each thought responds to the last observation. Voyager consumes execution progress, execution errors, and self-verification results. DEPS argues that a bare completion signal fails to correct planning errors, so it reports the reason for failure. LLM-Planner re-plans when objects mismatch. Inner Monologue returns success signals plus passive and active scene descriptions. Human feedback aligns the agent with human values and suppresses hallucination; Inner Monologue solicits scene descriptions from people and folds them into the prompt. Model feedback comes from the agent itself: self-refine iterates output, feedback, and refinement; SelfCheck audits reasoning steps; InterAct assigns auxiliary models as checkers and sorters; Reflexion replaces a scalar reward with verbal feedback from an evaluator over the trajectory.

### Action module

The action module sits furthest downstream and touches the environment. Four perspectives describe it. Action goal covers task completion, communication with agents or humans, and environment exploration. Action production covers two strategies: action via memory recollection, where retrieved records prompt the action, and action via plan following, where the agent adheres to a pre-generated plan unless a failure signal arrives. Action space splits into external tools and internal LLM knowledge. External tools include APIs, where HuggingGPT, WebGPT, Gorilla, Toolformer, ToolLLaMA, RestGPT, and TaskMatrix.AI sit; databases and knowledge bases, where ChatDB and MRKL sit; and external models, where ViperGPT generates and runs Python, ChemCrow calls 17 expert-designed models, and MM-REACT routes across video, image, and audio models. Internal knowledge supplies three capabilities: planning, conversation, and common sense understanding. Action impact covers changing the environment, altering internal state such as memory and plans, and triggering new actions.

### Capability acquisition

Fine-tuning routes split by dataset origin. Human-annotated data drives CoH, RET-LLM's triplet-to-language pairs, WebShop's collection of 1.18 million products with behaviour from 13 workers, and EduChat. LLM-generated data drives ToolBench, which prompts ChatGPT over 16,464 real-world APIs from RapidAPI Hub across 49 categories, then fine-tunes LLaMA. Real-world data drives MIND2WEB, built from over 2,000 open-ended tasks across 137 websites and 31 domains, and SQL-PaLM on Spider and BIRD.

Routes without fine-tuning cover prompt engineering and mechanism engineering. Prompt engineering writes the desired capability into the prompt, as CoT, CoT-SC, ToT, and RLP do, and Retroformer folds generated reflections back into the prompt under reinforcement learning. Mechanism engineering has four forms. Trial-and-error invokes a critic after each action and feeds its verdict forward, as RAH, DEPS, RoCo, and PREFER do. Crowd-sourcing debates responses across agents until consensus. Experience accumulation stores successful actions for reuse, as GITM, Voyager's skill library, AppAgent's knowledge base, and MemPrompt do. Self-driven evolution lets the agent set its own goals, as LMA3 and NLSOM do. Fine-tuning carries more task knowledge but needs an open-weight model. Prompt and mechanism routes work on closed models, yet the context window caps how much task information fits, and the design space resists search.

## Code Examples

The paper is a survey and carries no reusable code. It formalises memory reading as a weighted sum of recency, relevance, and importance scores under three balancing parameters, and it catalogues open-source libraries developers build on, including LangChain, XLang, AutoGPT, WorkGPT, GPT-Engineer, DemoGPT, AGiXT, AgentVerse, GPT Researcher, and BMTools.

## Best Practices

- Combine profile generation strategies. Ground part of the population in real data, then hand-assign the roles that data cannot supply.
- Choose hybrid memory for tasks needing long-range reasoning and accumulated experience. Unified memory suits short, context-sensitive interaction.
- Combine memory formats. Index with embeddings for retrieval speed and store values in natural language for comprehension.
- Handle duplication and overflow at write time. Condense similar records into one plan, and set an explicit eviction rule before storage fills.
- Report the reason for a failure, not the fact of it. A bare completion signal fails to correct a planning error.
- Combine feedback sources. Inner Monologue draws on environment and human feedback together.
- Delegate low-level control to an external planner where the LLM plans well and executes poorly.
- Combine subjective and objective evaluation. Neither measures the full range of agent capability alone.

## Warnings and Anti-Patterns

- Do not push comprehensive memory into the prompt under unified memory. The context window bounds it, and performance degrades.
- Do not rely on planning without feedback for long-horizon tasks. A plan written once from the start fails against unpredictable transition dynamics.
- Do not treat prompt frameworks as stable. Minor alterations shift outcomes, a prompt for one module perturbs others, and frameworks vary across models.
- Do not deploy a science assistant without domain expertise on hand. A hallucinating agent produces wrong conclusions, failed experiments, and physical risk in hazardous work.
- Do not ignore misuse. The authors flag chemical weapon development as an exploitation route, and call for human alignment as a security measure.
- Do not assume an LLM lacks knowledge a simulated user would lack. Web-scale training gives the model information the person it simulates never had, which corrupts the simulation.
- Do not rely on human annotation alone. It costs a lot, runs slow, and carries population bias.
- Do not overlook inference cost. An agent queries the model many times per action, so autoregressive decoding speed bounds throughput.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[agent-patterns-index]]
- [[the-agent-loop]]
- [[memory]]
- [[planning-and-reasoning]]
- [[plan-and-execute]]
- [[tool-use]]
- [[react]]
- [[reflexion]]
- [[prompt-engineering]]
- [[supervisor-worker-multi-agent]]
- [[evaluation]]
- [[agent-vs-llm]]
- [[workflow-vs-autonomous-agent]]
- [[10_Sources/Papers/agent-architectures-landscape-masterman-2024|Agent Architectures Landscape]]
- [[10_Sources/Papers/llm-agent-paradigms-review-li-2024|LLM Agent Paradigms Review]]
- [[10_Sources/Papers/llm-agent-planning-survey-huang-2024|LLM Agent Planning Survey]]
- [[10_Sources/Papers/react-yao-2022|ReAct]]
- [[10_Sources/Papers/reflexion-shinn-2023|Reflexion]]

## Future Work

The paper closes with six challenges. Role-playing capability suffers where a role appears rarely on the web or emerged after training, and existing models model human cognitive psychology poorly, so agents lack self-awareness in conversation. Fine-tuning on collected human data offers a route, at the risk of degrading common roles. Generalised human alignment asks how an agent aligns with diverse human values rather than one fixed set. A faithful simulator must depict harmful traits, since a simulation without negative behaviour surfaces no problem to solve, yet deployed models align to unified values. Prompt robustness asks how to build one resilient prompt framework across modules and across models. Hallucination produces false output with high confidence, which yields incorrect code, security risk, and ethical harm; human correction inside the interaction loop offers a mitigation. Knowledge boundary asks how to constrain an agent from using knowledge the simulated user never had. Efficiency remains bounded by autoregressive inference speed, since one agent action costs several model queries.

## References

- Canonical: https://doi.org/10.1007/s11704-024-40231-1
- Preprint: https://arxiv.org/abs/2308.11432
- Shinn N, Cassano F, Gopinath A, Narasimhan K, Yao S. "Reflexion: Language agents with verbal reinforcement learning." NeurIPS, 2024.
- Shen Y, Song K, Tan X, Li D, Lu W, Zhuang Y. "HuggingGPT: Solving AI tasks with ChatGPT and its friends in Hugging Face." NeurIPS, 2024.
- Qin Y, Liang S, Ye Y, Zhu K, Yan L, Lu Y, Lin Y, Cong X, Tang X, Qian B, et al. "ToolLLM: Facilitating large language models to master 16000+ real-world APIs." arXiv:2307.16789, 2023.
- Schick T, Dwivedi-Yu J, Dessì R, Raileanu R, Lomeli M, Hambro E, Zettlemoyer L, Cancedda N, Scialom T. "Toolformer: Language models can teach themselves to use tools." NeurIPS, 2024.
- Zhu X, Chen Y, Tian H, Tao C, Su W, Yang C, Huang G, Li B, Lu L, Wang X, et al. "Ghost in the Minecraft." arXiv:2305.17144, 2023.
- Qian C, Cong X, Yang C, Chen W, Su Y, Xu J, Liu Z, Sun M. "Communicative agents for software development." arXiv:2307.07924, 2023.
- Park J S, O'Brien J, Cai C J, Morris M R, Liang P, Bernstein M S. "Generative agents: Interactive simulacra of human behavior." UIST, 2023.
- Wang L, Zhang J, Chen X, Lin Y, Song R, Zhao W X, Wen J R. "RecAgent: A novel simulation paradigm for recommender systems." arXiv:2306.02552, 2023.
- Hong S, Zheng X, Chen J, Cheng Y, Wang J, Zhang C, Wang Z, Yau S K S, Lin Z, Zhou L, et al. "MetaGPT: Meta programming for multi-agent collaborative framework." arXiv:2308.00352, 2023.
