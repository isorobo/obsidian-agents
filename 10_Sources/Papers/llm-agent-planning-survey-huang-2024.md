---
type: source
status: draft
created: 2026-07-10
title: "Understanding the Planning of LLM Agents: A Survey"
authors:
- Xu Huang
- Weiwen Liu
- Xiaolong Chen
- Xingmei Wang
- Hao Wang
- Defu Lian
- Yasheng Wang
- Ruiming Tang
- Enhong Chen
organisation: University of Science and Technology of China; Huawei Noah's Ark Lab
source_type: paper
venue: 
url: https://arxiv.org/abs/2402.02716
year: 2024
date_published: 2024-02-05
anthropic: false
topic:
- topic/planning
- topic/research-papers
tags: [planning, survey, task-decomposition, reflection, memory]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Understanding the Planning of LLM Agents: A Survey

> Full citation: Xu Huang, Weiwen Liu, Xiaolong Chen, Xingmei Wang, Hao Wang, Defu Lian, Yasheng Wang, Ruiming Tang, Enhong Chen. "Understanding the Planning of LLM Agents: A Survey." arXiv preprint, 2024. https://arxiv.org/abs/2402.02716

## Summary

This survey gives the first systematic view of planning in LLM-based agents. The authors define planning as the generation of an action sequence from an environment, a goal, and the model's parameters and prompts. They group existing work into five directions: task decomposition, multi-plan selection, external planner-aided planning, reflection and refinement, and memory-augmented planning. Each direction gets a formal process definition, representative methods, and a discussion of trade-offs. The paper also runs experiments on four interactive benchmarks (ALFWorld, ScienceWorld, HotPotQA, FEVER), comparing six prompt-based methods on success rate, reward, and token expense. It closes with five open challenges: hallucination, feasibility of generated plans, efficiency of generated plans, multi-modal environment feedback, and the lack of fine-grained evaluation.

## Key Concepts

- Planning is formalised as `p = (a0, a1, ..., at) = plan(E, g; Θ, P)`, a sequence of actions produced from an environment E, a goal g, model parameters Θ, and prompts P.
- Task decomposition splits into decomposition-first (plan sub-goals up front, then solve each) and interleaved (decompose and act one step at a time, adjusting to feedback).
- Multi-plan selection generates several candidate plans, then applies a search or voting strategy to pick one.
- External planner-aided planning offloads plan generation to a symbolic solver (for example, PDDL) or a neural planner, with the LLM formalising the task.
- Reflection and refinement lets the agent evaluate its own trajectory, generate a verbal self-critique, and revise the plan.
- Memory-augmented planning retrieves stored experience, either via retrieval-augmented generation over an external store, or via fine-tuning the model on past trajectories (embodied memory).

## Terminology

- **Decomposition-first**: sub-goals are fixed before any sub-plan executes.
- **Interleaved decomposition**: decomposition and execution alternate, revealing one or two sub-goals at a time.
- **Multi-plan generation**: sampling or prompting the LLM to produce several candidate plans for the same goal.
- **Symbolic planner**: a classical solver, such as a PDDL-based planner, that finds a plan once the LLM has formalised the task into its input format.
- **Neural planner**: a trained policy model, such as a Decision Transformer, that generates or re-ranks actions.
- **Embodied memory**: memory encoded into model parameters through fine-tuning on past trajectories, as opposed to memory held in an external store.
- **RAG-based memory**: memory held outside the model, retrieved by similarity to the current state and injected into the prompt.

## Architecture and Implementation

The survey's core contribution is the five-way taxonomy, not a single system architecture. Task Decomposition treats a complex goal as a divide-and-conquer problem: the LLM produces sub-goals, then solves each in turn, either fully up front or interleaved with execution and feedback. Plan Selection (called Multi-plan Selection in the paper) treats planning as a search problem: the LLM proposes multiple candidate plans, and a search or voting strategy, such as majority vote, tree search, or Monte Carlo Tree Search, selects the plan to execute. External Module (External Planner-Aided Planning) hands the actual search to a symbolic or neural planner outside the LLM; the LLM's job narrows to formalising the natural-language task into the planner's input format. Reflection treats planning as an iterative loop of generation, evaluation, and refinement, where the LLM critiques its own trajectory in natural language and produces a revised plan. Memory augments any of the above with a retrieval step, either pulling relevant past experience from an external store before planning, or embedding that experience into the model weights through fine-tuning. The paper stresses that these five directions combine rather than compete. Most cited systems, such as ReAct and Reflexion, draw on more than one.

## Code Examples

This is a survey paper; it does not ship code. It references implementations of the systems it surveys, including ReAct, Tree-of-Thought, Reflexion, and MemGPT, but provides no code of its own.

## Best Practices

- Match the decomposition style to the task. Decomposition-first suits tasks where sub-goals stay stable, since it strengthens the link between sub-tasks and the original goal. Interleaved decomposition suits tasks with unpredictable feedback, since it adjusts sub-goals as the environment responds.
- Use few-shot examples over zero-shot instructions for complicated tasks. The paper's own benchmark results show Zero-shot CoT degrading badly on question-answering tasks compared with few-shot CoT.
- Add reflection for complex, multi-step tasks. The benchmark experiments show Reflexion delivering the largest success-rate gains on the hardest tasks, ALFWorld and ScienceWorld, despite roughly doubling token cost over ReAct.
- Treat symbolic planners as a complement to the LLM, not a replacement. The LLM formalises the problem; the solver guarantees completeness and stability that pure LLM search cannot.

## Warnings and Anti-Patterns

- Multi-plan selection and reflection both raise token cost, and the paper's experiments show performance rising with expense. Budget-constrained deployments need to weigh this trade-off directly.
- Decomposition-first methods fail outright if an early sub-goal is wrong, since nothing downstream revisits it. The paper flags this as a fault-tolerance gap requiring extra adjustment mechanisms.
- Long interleaved trajectories risk hallucination and drift from the original goal as context grows.
- LLM-based plan evaluation, used in several multi-plan selection methods, is unreliable. The paper notes that LLM ranking ability is still under scrutiny, and the stochastic nature of LLM output adds inconsistency to plan selection.
- Reflection's textual self-update has no convergence guarantee. Unlike gradient-based reinforcement learning, there is no proof that repeated self-reflection converges the agent toward the goal.
- Most existing benchmarks score only final task success, not intermediate plan quality, and typically offer a single "golden" path, which understates the real-world diversity of valid plans.

## Related Concepts

- [[planning-and-reasoning]]
- [[reflexion]]
- [[memory]]
- [[react]]
- [[plan-and-execute]]

## Future Work

The authors name five open challenges. Hallucination causes irrational plans and actions that reference non-existent items in the environment. Feasibility suffers because LLMs optimise next-word probability rather than obeying hard constraints, making symbolic-planner integration a promising fix. Efficiency of generated plans is largely ignored, since most agents greedily accept the first plan produced without an efficiency check. Multi-modal environment feedback, such as images and audio, is hard for text-native LLMs to consume, pointing toward tighter integration with multi-modal models. Fine-grained evaluation is missing, since most benchmarks report only end-task success rather than step-wise plan quality, and the authors suggest using capable LLMs to design richer evaluation environments.

## References

- Wei, J. et al. "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models." NeurIPS, 2022.
- Yao, S. et al. "ReAct: Synergizing Reasoning and Acting in Language Models." arXiv:2210.03629, 2022.
- Shinn, N. et al. "Reflexion: Language Agents with Verbal Reinforcement Learning." NeurIPS, 2023.
- Yao, S. et al. "Tree of Thoughts: Deliberate Problem Solving with Large Language Models." arXiv:2305.10601, 2023.
- Packer, C. et al. "MemGPT: Towards LLMs as Operating Systems." arXiv:2310.08560, 2023.
- Park, J. S. et al. "Generative Agents: Interactive Simulacra of Human Behavior." UIST, 2023.
- Liu, B. et al. "LLM+P: Empowering Large Language Models with Optimal Planning Proficiency." arXiv:2304.11477, 2023.
- Madaan, A. et al. "Self-Refine: Iterative Refinement with Self-Feedback." arXiv:2303.17651, 2023.
