---
type: source
status: draft
created: 2026-07-10
title: "Survey on Evaluation of LLM-based Agents"
authors:
- Asaf Yehudai
- Lilach Eden
- Alan Li
- Guy Uziel
- Yilun Zhao
- Roy Bar-Haim
- Arman Cohan
- Michal Shmueli-Scheuer
organisation: IBM Research
source_type: paper
venue: 
url: https://arxiv.org/abs/2503.16416
year: 2025
date_published: 2025-03-20
anthropic: false
topic:
- topic/evaluation
- topic/research-papers
tags: [evaluation, benchmarks, agent-metrics, survey, agent-harness]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Survey on Evaluation of LLM-based Agents

> Full citation: Asaf Yehudai, Lilach Eden, Alan Li, Guy Uziel, Yilun Zhao, Roy Bar-Haim, Arman Cohan, and Michal Shmueli-Scheuer. "Survey on Evaluation of LLM-based Agents." arXiv, 2025. https://arxiv.org/abs/2503.16416

## Summary

This paper is the first comprehensive survey of evaluation methods for LLM-based agents. The authors, from IBM Research, the Hebrew University of Jerusalem, and Yale University, argue that agents demand a different evaluation paradigm than static language models. An agent plans, calls tools, and adapts across a sequence of actions inside a changing environment, so a benchmark must judge sequential decision-making, not a single text output. The survey organises the field into five perspectives: core LLM capabilities that underpin agentic behaviour, benchmarks tied to specific applications, evaluation of generalist agents, the shared structural dimensions that cut across benchmarks, and the development frameworks that practitioners use to monitor and test agents. Across these perspectives, the authors trace a shift from simplified, static test setups toward realistic, dynamic, and continuously updated benchmarks. They close by naming persistent gaps: coarse-grained success metrics that hide where an agent fails, absent cost-efficiency tracking, weak safety and compliance testing, and a failure to separate the backbone model's capability from the surrounding agent harness.

## Key Concepts

- Agent evaluation must assess sequential decision-making inside a dynamic environment, not a single text output.
- An agent's performance conflates two distinct factors: the backbone LLM's capability and the design of the agent harness (scaffold) around it.
- Benchmarks increasingly move from static, offline traces toward dynamic environments where an agent's actions change the state it observes.
- Live benchmarks that update over time (for example, successive BFCL and SWE-bench versions) resist saturation and obsolescence.
- Coarse, binary task-completion metrics obscure intermediate failures in tool selection, planning, and reasoning.

## Terminology

- **Agent harness (scaffold)** — the surrounding system (prompting strategy, tool orchestration, memory management) that wraps a backbone LLM to produce agentic behaviour.
- **Static environment** — an evaluation setting using offline traces or cached state, where an agent's actions do not alter what it observes next.
- **Dynamic environment** — a live or simulated setting where an agent's actions change subsequent state, surfacing compounding failures over a task.
- **Reference-based trajectory assessment** — scoring an agent's action sequence against a predefined gold path.
- **Reference-free trajectory assessment** — scoring an agent's action sequence with an LLM judge, without a predefined gold path.
- **Pass^k** — a robustness metric measuring the fraction of tasks an agent solves correctly across all k independent runs.

## Architecture and Implementation

The survey structures the evaluation landscape around five perspectives.

**Core LLM capabilities** covers the abilities an agentic workflow depends on: planning and multi-step reasoning, function calling and tool use, self-reflection, and memory. Each capability can be tested in isolation, using benchmarks such as PlanBench for planning or the Berkeley Function Calling Leaderboard for tool use, or as part of a full agent run.

**Application-specific benchmarks** evaluate agents built for a defined task family. The survey reviews web agents (WebArena, Mind2Web), software engineering agents (SWE-bench and its verified and pro variants), scientific agents (SciCode, PaperBench), and conversational agents (tau-Bench). Each family has moved from narrow, simulated tasks toward benchmarks grounded in real repositories, websites, or freelance work.

**Generalist-agent evaluation** covers two approaches to testing agents across many capabilities at once: benchmarks that inherently demand a wide skill range in one environment, such as Gaia and Gaia2, and frameworks that unify several task-specific benchmarks under one harness, such as AgentBench and the Holistic Agent Leaderboard.

**Benchmark-dimension analysis** steps back from individual benchmarks to compare them along shared axes: how data is curated (human-only, synthetic, or hybrid), whether the environment is static or dynamic, what interface the agent uses (code and terminal, tool calls, or a graphical interface), what metric defines success (unit tests, state matching, or answer matching), and whether safety constraints are tested at all. Most benchmarks in the survey's comparison table do not test safety.

**Evaluation frameworks and tools** covers the platforms developers use during building and deployment, such as LangSmith, Langfuse, and Google Vertex AI evaluation. These support final-response evaluation, stepwise evaluation of individual agent actions, and trajectory-based assessment of the full action sequence, plus supporting features such as human-in-the-loop annotation and synthetic data generation.

## Code Examples

Not applicable. The paper is a survey and contains no code.

## Best Practices

- Test agent capabilities such as planning and tool use both in isolation and as part of a full workflow, since isolated results do not always predict end-to-end performance.
- Prefer dynamic environments over static traces when the goal is to diagnose compounding, long-horizon failures.
- Combine stepwise evaluation with trajectory-based assessment to catch both isolated action errors and dependencies between steps.
- Track cost and efficiency (token usage, latency, API expense) alongside task success, since capability-only metrics reward resource-intensive agents.
- Separate the backbone LLM's contribution from the agent harness's contribution wherever the evaluation setup allows it.

## Warnings and Anti-Patterns

- Relying on coarse, binary task-completion metrics hides where and why an agent fails inside a multi-step trajectory.
- Static, offline benchmarks miss compounding failures, since an incorrect early action carries no downstream consequence.
- Reference-based trajectory scoring assumes a single correct path, which understates agents that reach the goal by a valid alternative route.
- Treating a benchmark as permanent invites saturation. Capable models eventually top out on a fixed benchmark, so evaluation regimes need periodic refresh.
- Omitting safety and policy-compliance checks lets an agent pass a benchmark through non-compliant actions, such as an unsafe database operation, that the metric does not penalise.

## Related Concepts

- [[evaluation]]
- [[the-agent-loop]]
- [[tool-use]]
- [[planning-and-reasoning]]
- [[memory]]

## Future Work

The authors name four priorities for the field. First, fine-grained evaluation methods that assess an agent's trajectory step by step, rather than only its final outcome. Second, standardised cost-efficiency metrics covering token usage, inference time, and API expense, so evaluation does not reward resource-intensive agents by default. Third, scalable and automated evaluation, through synthetic data generation and LLM-as-judge techniques, to reduce dependence on costly human annotation. Fourth, stronger safety and compliance testing, including robustness to adversarial input and multi-agent risk, and evaluation protocols that isolate the backbone LLM's contribution from the agent harness's contribution to overall performance.

## References

- Yehudai, A., Eden, L., Li, A., Uziel, G., Zhao, Y., Bar-Haim, R., Cohan, A., and Shmueli-Scheuer, M. "Survey on Evaluation of LLM-based Agents." arXiv:2503.16416, 2025. https://arxiv.org/abs/2503.16416
