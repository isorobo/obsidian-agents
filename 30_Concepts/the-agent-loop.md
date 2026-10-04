---
type: concept
status: draft
created: 2026-07-10
name: The Agent Loop
slug: the-agent-loop
topic:
- topic/foundations
- topic/architectures
tags:
- agents
- loop
- control-flow
synonyms:
- agentic loop
- agent execution loop
- perceive-decide-act loop
defined_in: "[[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]"
related_concepts:
- "[[what-is-an-ai-agent]]"
- "[[tool-use]]"
- "[[react]]"
af_targets:
- af:ADR-0001
- af:RSCH-04/Q01
- af:RSCH-04/Q13
wiki_indexed: '2026-10-04T03:42:35Z'
wiki_hash: 3dd04b33399ef34052378b028ca712cd025c71dafd257850724c5729bd7936f7
---

# The Agent Loop

> The agent loop is the repeating cycle in which a model reads context, chooses an action, calls a tool, and reads the result until the task closes.

## Summary

The agent loop is the engine of every agent. Anthropic describes agents running in a loop, using tools based on environment feedback at each step. The environment returns ground truth, such as a tool result or code output. The model reads that truth, judges progress, and picks the next move. The loop ends at a stop condition or a human checkpoint. This cycle turns a one-shot model into a system that acts over time.

## Key Concepts

- The loop repeats read, decide, act, and observe.
- Environment feedback grounds each step in ground truth.
- A stop condition or checkpoint closes the loop.
- The loop carries state that a single model call lacks.

## Detail

The loop runs four moves. First, the model reads the current context and the goal. Second, the model decides the next action. Third, the harness runs the action as a tool call. Fourth, the environment returns a result that rejoins the context. The cycle then repeats with richer context.

ReAct names the pattern behind the loop. It interleaves reasoning traces with actions. The reasoning tracks the plan and handles exceptions. The action gathers information from the world. The loop needs a guard. A step budget or a goal test stops runaway cycles. A human checkpoint holds the loop at a blocker or a risky action.

## Trade-offs and Limits

The loop gives recovery, since the model reads each result and adjusts. It handles branches a fixed script cannot foresee. The loop can also stall, repeat, or drift on a hard task. Every turn adds tokens and latency. Guards and budgets keep the loop bounded and legible.

## Related

- [[what-is-an-ai-agent]]
- [[tool-use]]
- [[react]]
- [[planning-and-reasoning]]

## Sources

- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]
- ReAct: Synergizing Reasoning and Acting in Language Models — https://arxiv.org/abs/2210.03629
- [[10_Sources/Blog/anthropic-scaling-managed-agents|Scaling Managed Agents]]
- [[10_Sources/Blog/loop-engineering-anthropic-playbook|Loop Engineering: The Anthropic Playbook]]
- [[10_Sources/Blog/harness-six-components|The 6 Components of a Production Agent Harness]]
- [[10_Sources/Blog/how-to-evaluate-ai-agents|How to Evaluate AI Agents]]
- [[10_Sources/Papers/mid-harness-kang-2026|Mid-Harness (Kang et al., 2026)]]
- [[10_Sources/Papers/coala-cognitive-architectures-sumers-2023|CoALA (Sumers et al., 2023)]]
- [[10_Sources/Papers/refcon-contrastive-memory-prathama-2026|RefCon (Prathama et al., 2026)]]
- [[10_Sources/Papers/swe-agent-computer-interfaces-yang-2024|SWE-agent (Yang et al., 2024)]]
- [[10_Sources/Docs/claude-agent-sdk-hooks|Agent SDK hooks]]
- [[10_Sources/Repos/12-factor-agents|12-Factor Agents]]
- [[10_Sources/Repos/claude-agent-sdk-python|Claude Agent SDK for Python]]
- [[10_Sources/Repos/learn-agent-architecture|learn-agent-architecture]]
- [[10_Sources/Repos/mini-swe-agent|mini-SWE-agent]]
- [[10_Sources/Repos/smolagents|smolagents]]

## See also

- [[MOC - Architectures]]
- [[MOC - Foundations]]
