---
type: source
status: draft
created: 2026-07-10
title: "AI Agent Systems: Architectures, Applications, and Evaluation"
authors:
- Bin Xu
organisation: "School of Electrical, Computer and Energy Engineering, Arizona State University"
source_type: paper
venue: 
url: https://arxiv.org/abs/2601.01743
year: 2026
date_published: 2026-01-05
anthropic: false
topic:
- topic/architectures
- topic/research-papers
tags: [survey, taxonomy, orchestration, evaluation]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# AI Agent Systems: Architectures, Applications, and Evaluation

> Full citation: Xu, B. "AI Agent Systems: Architectures, Applications, and Evaluation." arXiv:2601.01743, 2026. https://arxiv.org/abs/2601.01743

## Summary

This survey maps the emerging landscape of AI agent architectures, systems that combine foundation models with reasoning, planning, memory, and tool use. Xu organises prior work along three axes: deliberation and reasoning, including chain-of-thought-style decomposition, self-reflection, and constraint-aware decision making; planning and control, spanning reactive policies through hierarchical and multi-step planners; and tool calling and environment interaction, covering retrieval, code execution, APIs, and multimodal perception. The paper builds a unified taxonomy across agent components, orchestration patterns, and deployment settings, then examines the design trade-offs that shape agent behaviour and the practices used to measure it. The survey closes on open challenges: verification and guardrails for tool actions, scalable memory and context management, interpretability of agent decisions, and reproducible evaluation under realistic workloads.

## Key Concepts

- An agent combines a foundation model with reasoning, planning, memory, and tool use.
- The taxonomy spans agent components, orchestration patterns, and deployment settings.
- Design trade-offs govern agent behaviour: latency against accuracy, autonomy against controllability, and capability against reliability.
- Evaluation is complicated by non-determinism, long-horizon credit assignment, tool and environment variability, and hidden costs such as retries and context growth.

## Terminology

- **Agent transformer** — Xu's formal model of an agent: a tuple A = (π, M, T, V, E), where π is the transformer policy, M is memory, T is the tool set, V is the verifier or critic set, and E is the environment.
- **Policy or LLM core** — the model component that selects the agent's next action.
- **World model** — the component that represents the state of the agent's environment.
- **Tool router** — the component that selects and invokes external tools, APIs, or retrieval systems; MRKL-style systems route tasks to specialised tools, separating language understanding from deterministic components.
- **Critic** — the component that verifies an agent's proposed or completed actions; Xu treats verifiers as defining the agent's operational semantics, not as an optional add-on.
- **Centralised coordination** — a multi-agent pattern in which one controller directs subordinate agents.
- **Decentralised coordination** — a multi-agent pattern in which agents coordinate without a single controller.

## Architecture and Implementation

Xu formalises an agent as an "agent transformer": a tuple A = (π, M, T, V, E), where π is a transformer-based policy, M is memory (retrieval, summaries, running state), T is a typed tool set (APIs, code execution, search, databases), V is a set of verifiers or critics, and E is the environment. The execution loop observes the environment, retrieves relevant memory, proposes an action through the policy, validates that action against the verifiers, then executes and updates memory. The survey gives a practical build recipe on top of this formalism: typed tool schemas, an explicit control loop, a separated planner and executor, and a trace-first data flywheel that logs trajectories for later improvement.

The taxonomy layers two further axes on top of this formal core. Orchestration patterns split agents into single-agent and multi-agent systems; multi-agent coordination is developed most fully in the survey's discussion of role specialisation, where planner, executor, and reviewer roles carry bounded tool permissions, and multi-agent debate carries a risk of correlated blind spots across agents built on similar base models. Deployment settings split offline analysis from online interactive assistance, and safety-critical tasks from open-ended tasks. Cost and latency trade-offs run through the whole taxonomy, since multi-step tool use can require many model calls, and Xu frames budgeted autonomy, policies that scale planning depth and verification intensity to risk and uncertainty, as the practical response.

## Code Examples

This is a survey paper. It carries a formal notation (a numbered tuple model and evaluation equations) rather than code listings, and it does not link an accompanying repository.

## Best Practices

- Select an orchestration pattern, single-agent or multi-agent, centralised or decentralised, to match the task's coordination needs rather than by default.
- Match deployment setting to task risk: reserve open-ended, high-autonomy configurations for tasks that tolerate error, and constrain safety-critical tasks with tighter controllability.
- Budget autonomy: scale planning depth and verification intensity to the risk and uncertainty of the task, rather than applying uniform scrutiny everywhere.
- Treat verifiers and critics as part of the agent's operational semantics, not an optional add-on, per Xu's own framing.
- Budget for hidden evaluation costs, including retries and context growth, when measuring agent performance, not only for task success.

## Warnings and Anti-Patterns

Xu names three design trade-offs that recur across agent architectures: latency against accuracy, autonomy against controllability, and capability against reliability. A system tuned for one side of each trade-off degrades on the other, so a design choice made for one deployment setting may not transfer to another.

Evaluation carries its own complications, developed across six dimensions in the survey: end-to-end task performance, efficiency and cost (latency, token cost, retries), tool-use correctness, trajectory and planning quality, robustness (including variance across random seeds), and safety and compliance, benchmarked against suites such as AgentBench, WebArena, ToolBench, SWE-bench, and GAIA. Non-determinism in sampling and in tool responses makes failures hard to reproduce. Long-horizon tasks complicate credit assignment, since a failure late in a trajectory may trace back to an early decision, and errors compound over long trajectories. Multi-agent debate risks correlated blind spots when agents share a base model. A benchmark that ignores these factors overstates an agent's reliability.

## Related Concepts

- [[the-agent-loop]]
- [[tool-use]]
- [[memory]]
- [[planning-and-reasoning]]
- [[supervisor-worker-multi-agent]]
- [[evaluation]]

## Future Work

Xu closes on six directions: verification and trustworthy tool execution; long-term memory and context management; planning and test-time compute allocation; robust evaluation and reproducibility; multi-agent coordination and governance, including observability, audit logs, and incident response; and a push toward unified conceptual frameworks that settle the terminology gap between "agent" and "agentic workflow". The conclusion frames the central research challenge as making agent autonomy dependable at scale: verifiable, policy-compliant tool execution; secure and consistent long-term memory; principled allocation of test-time compute under explicit budgets; and trace-first observability.

## References

- Xu, B. "AI Agent Systems: Architectures, Applications, and Evaluation." arXiv:2601.01743, 2026. https://arxiv.org/abs/2601.01743
