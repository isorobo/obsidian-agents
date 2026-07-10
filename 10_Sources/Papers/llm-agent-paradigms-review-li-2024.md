---
type: source
status: draft
created: 2026-07-10
title: "A Review of Prominent Paradigms for LLM-Based Agents: Tool Use (Including RAG), Planning, and Feedback Learning"
authors:
- Xinzhe Li
organisation: 
source_type: paper
venue: 
url: https://arxiv.org/abs/2406.05804
year: 2024
date_published: 2024-06-09
anthropic: false
topic:
- topic/tool-use
- topic/planning
- topic/research-papers
tags: [tool-use, rag, feedback-learning, taxonomy, planning]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# A Review of Prominent Paradigms for LLM-Based Agents: Tool Use (Including RAG), Planning, and Feedback Learning

> Full citation: Xinzhe Li. "A Review of Prominent Paradigms for LLM-Based Agents: Tool Use (Including RAG), Planning, and Feedback Learning." arXiv, 2024. https://arxiv.org/abs/2406.05804

## Summary

Prior surveys of LLM-based agents cover one paradigm or one domain, such as planning alone or games alone. They give no shared basis for comparing tool use, planning, and feedback learning as a set. This paper builds a unified taxonomy on two task-agnostic layers. The first layer sorts environments and tasks, from rule-based games through embodied and web environments to natural language interaction environments, its own term for language tasks reframed as agentic settings. The second layer defines LLM-Profiled Roles: a policy that decides, an evaluator that scores or revises, and a dynamic model that predicts environment change. The paper derives workflows from these roles and uses the workflows, not the domain, to compare frameworks across all three paradigms. It distinguishes a framework, a full pipeline built for one task, from a workflow, the task-agnostic process a reader can abstract from one or more frameworks. The review closes by naming three limitations in current workflow design and by arguing that new workflows should combine existing ones within and across paradigms, since validation-style tool use already blends tool use and feedback learning.

## Key Concepts

- Two task-agnostic environment classes: feedback-based decision-making environments and information processing environments, the second split into web environments and natural language interaction environments.
- Three LLM-Profiled Roles: policy (actor or planner), evaluator, and dynamic model.
- A workflow is the task-agnostic process; a framework is the full pipeline built for one task.
- Tool use, planning, and feedback learning overlap. Validation-based tool use is a form of feedback learning.

## Terminology

- LLM-Profiled Role (LMPR) — a task-agnostic functional role an LLM fills inside a workflow.
- Policy (g_lm,policy) — the LMPR that generates a decision, either an action (actor) or a plan (planner).
- Evaluator (g_lm,eval) — the LMPR that scores, selects, or revises a decision.
- Dynamic model (g_lm,dynamic) — the LMPR that predicts or describes how the environment changes after an action.
- Natural Language Interaction Environment (NLIE) — the paper's term for an NLP task reframed as a single-step or multi-step decision problem.
- Base workflow — the simplest workflow: policy acting on the environment alone, with no tool or evaluator layer.

## Architecture and Implementation

The taxonomy has three tiers. The first tier sorts environments into feedback-based decision-making environments, such as rule-based games and embodied simulators, and information processing environments, such as web environments and NLIEs. NLIEs split further into single-step forms, where a QA task becomes a one-shot decision, and deliberate multi-step forms, where a task becomes a Markov decision process through subquestion decomposition or a planning-then-execution split.

The second tier defines the three LMPRs stated above. The paper builds every workflow from these three roles rather than from named agent products, which lets it compare frameworks across domains on the same footing.

The third tier derives four workflow families from the roles. Base workflows connect only the policy to the environment, in planner or actor form. Tool-use workflows add an external tool and split into passive forms, RAG-style retrieval and passive validation, and autonomous forms, where the policy or evaluator decides on its own whether to invoke a tool. Search workflows add exploration for planning: traversal and heuristic-based search, such as Tree-of-Thoughts, expands a tree or graph under a fixed evaluator score, while simulation-based search, Monte Carlo Tree Search, adds the dynamic model and a roll-out phase, then executes only the root action in the real environment. Feedback-learning workflows route a signal back into the policy for revision, and the paper sorts them by feedback source: the evaluator alone, the evaluator and the task environment together, a human, or a tool.

The paper reports this taxonomy as single-agent throughout. It does not propose a separate multi-agent or sequential-versus-parallel workflow layer; each LMPR sits inside one agent loop, even where a framework names its roles as if they were separate agents.

## Code Examples

The paper carries no code. It states its workflows as role interactions and cites the released implementations of the surveyed frameworks, such as ReAct, Reflexion, and Tree-of-Thoughts, as the concrete realisations of each workflow type.

## Best Practices

- Compare agent frameworks by the workflow they realise, not by the domain they target.
- Treat retrieval-augmented generation as one instance of passive tool use, not a separate paradigm.
- Reserve ground-truth labels as a feedback source for baseline evaluation, since they are unrealistic as a feedback source in a deployed setting.
- Check whether a validation step already blends tool use and feedback learning before treating them as separate design choices.

## Warnings and Anti-Patterns

- Confidence-based tool triggers, as in Active RAG, name a mechanism specific to retrieval and do not generalise to arbitrary tool selection.
- Full-execution search plans, such as beam or tree search output, can propose an unexecutable action in a stochastic environment, unlike MCTS, which only commits the simulated root action.
- Framing ReAct's reasoning-acting alternation as a universal unification of tool use and base workflows overstates the case. The alternation is fixed and prompt-driven for QA tasks, but decided by the policy itself in embodied tasks.
- Ground-truth labels as feedback, used in some cited frameworks, work only as an evaluation baseline and misrepresent feedback learning in a real deployment.

## Related Concepts

- [[tool-use]]
- [[planning-and-reasoning]]
- [[react]]
- [[reflexion]]
- [[plan-and-execute]]

## Future Work

The paper names three limitations. First, no unified workflow yet spans base workflows and autonomous tool-use workflows; ReAct's attempt folds tool actions and task actions into one format, but the two remain distinct in practice. Second, no general-purpose tool-use workflow exists; current work narrows tool use to NLIE-QA retrieval or to validation, rather than open-ended tool selection. Third, the practice of reframing language tasks as agentic tasks carries open problems, including the use of ground-truth labels as feedback and unclear rules for when a question needs multi-step decomposition at all. The paper argues new workflows should combine existing ones, within a paradigm or across paradigms, since validation-based tool use already merges tool use with feedback learning. Its own stated limitation is coverage: due to length, it surveys representative and pioneering work mainly from ACL, ICML, ICLR, and NeurIPS, and it sets aside task-specific components, such as the vision model an embodied-environment agent needs to turn pixels into text for its policy.

## References

- https://arxiv.org/abs/2406.05804
