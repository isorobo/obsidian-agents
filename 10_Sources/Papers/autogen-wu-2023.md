---
type: source
status: draft
created: 2026-07-10
title: "AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation"
authors:
- Qingyun Wu
- Gagan Bansal
- Jieyu Zhang
- Yiran Wu
- Beibin Li
- Erkang Zhu
- Li Jiang
- Xiaoyun Zhang
- Shaokun Zhang
- Jiale Liu
- Ahmed Hassan Awadallah
- Ryen W White
- Doug Burger
- Chi Wang
organisation: Microsoft
source_type: paper
venue: 
url: https://arxiv.org/abs/2308.08155
year: 2023
date_published: 2023-08-16
anthropic: false
topic:
- topic/multi-agent
- topic/research-papers
tags: [multi-agent, conversation, framework, orchestration, tool-use]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation

> Full citation: Qingyun Wu, Gagan Bansal, Jieyu Zhang, Yiran Wu, Beibin Li, Erkang Zhu, Li Jiang, Xiaoyun Zhang, Shaokun Zhang, Jiale Liu, Ahmed Hassan Awadallah, Ryen W. White, Doug Burger, and Chi Wang. "AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation." arXiv, 2023. https://arxiv.org/abs/2308.08155

## Summary

The paper addresses two open design questions in multi-agent LLM development: how to build individual agents that are capable, reusable, and effective in collaboration, and how to give those agents a unified interface for a wide range of conversation patterns. AutoGen answers both with a generic, open-source framework built on one abstraction, the conversable agent, and one control model, conversation-driven orchestration. Agents combine three capability sources, language models, humans, and tools, and applications assemble multiple agents whose interaction pattern emerges from their conversation rather than a fixed pipeline. The authors demonstrate the framework across six application domains, from autonomous maths problem solving to conversational chess, and report that the conversation abstraction lets a developer reuse the same small set of agent classes across markedly different tasks.

## Key Concepts

- Conversable agent: an entity with a role that sends and receives messages, holds internal context from that exchange, and draws on LLM, human, and tool capabilities.
- Conversation-driven control: agent decisions about whom to message and what computation to run are functions of the conversation itself, not a hardcoded pipeline.
- Auto-reply mechanism: an agent that receives a message automatically invokes its reply generation and returns a response, unless a termination condition fires.
- Static and dynamic conversation topology: a workflow can follow a predefined agent sequence or select the next speaker at runtime.

## Terminology

- ConversableAgent: the base class that composes LLM, human, and tool capabilities behind one interface.
- AssistantAgent: a built-in ConversableAgent subclass configured as an LLM-backed AI assistant.
- UserProxyAgent: a built-in ConversableAgent subclass that solicits human input or executes tools on a human's behalf.
- GroupChatManager: an agent that coordinates a group chat, selecting the next speaker and broadcasting replies.
- human_input_mode: a configuration setting (`ALWAYS`, `NEVER`, or conditional) that controls how often an agent asks for human input.

## Architecture and Implementation

AutoGen defines applications in two steps. A developer first defines a set of conversable agents, each carrying a role and a capability mix of language models, human input, and tool execution. The developer then programs the interaction behaviour between agents through conversation-centric computation, rather than through a fixed call graph. The core mechanism is the auto-reply: once an agent receives a message, it invokes `generate_reply` and sends the result back to the sender unless a termination condition applies. Control logic can be expressed in natural language through an agent's system prompt, in Python through a registered reply function, or as a mix of both, with the LLM handing off to code and back within a single conversation.

The framework supports both static and dynamic conversation topology. A static topology fixes the agent sequence in advance, suited to well-understood workflows such as a two-agent chat. A dynamic topology lets the next speaker be chosen at runtime, through a customised reply function, an LLM function call, or the built-in `GroupChatManager`, which selects the next speaker and broadcasts its response to the rest of the group. This split lets a simple task run as a fixed pipeline while a complex task, such as the paper's dynamic group chat case study, adapts its own flow as the conversation unfolds.

## Code Examples

The paper illustrates the interface through a schematic figure rather than a runnable listing. It shows two agents, A and B, started with `A.initiate_chat(message, B)`, and a custom reply function registered with `A.register_reply(B, reply_func_A2B)`. Agent configuration is shown conceptually, with attributes such as `human_input_mode="NEVER"`, `human_input_mode="ALWAYS"`, and `code_execution_config=False`. The paper also reproduces the default system message used to configure `AssistantAgent` in the released library. The framework is open-source at https://github.com/microsoft/autogen.

## Best Practices

The authors set out five guidelines in their appendix. Start with the built-in `AssistantAgent` and `UserProxyAgent` before writing a custom agent class. Start with a simple conversation topology, such as a two-agent chat, before moving to a group chat. Reuse the built-in LLM, tool, or human reply methods before implementing a custom reply function. Keep a human in the loop during development, with `human_input_mode="ALWAYS"`, then relax to `"NEVER"` once the workflow is trusted. Recognise when a unidirectional pipeline library, such as LangChain or Semantic Kernel, better suits a task than a conversational multi-agent framework, and wrap such a library as a tool backend where useful.

## Warnings and Anti-Patterns

- Scaling the number of agents risks "incomprehensible, unintelligible chatter" that a developer cannot audit.
- Full autonomy raises safety risk in high-stakes applications and needs fail-safes against cascading failures and reward hacking.
- The authors cite CAMEL's role-play-only design as evidence that conversation without tool or code execution is not sufficient for capable agent behaviour.
- Code execution capability introduces its own risk, such as an agent installing packages, and needs the same scrutiny as any other tool grant.

## Related Concepts

- [[supervisor-worker-multi-agent]]
- [[tool-use]]
- [[the-agent-loop]]
- [[workflow-vs-autonomous-agent]]

## Future Work

Appendix B.2 names three open directions: designing optimal multi-agent workflows, since no single agent topology or role assignment fits every task; creating more capable individual agents, since conversation alone does not guarantee task success; and enabling scale, safety, and human agency together, so that larger agent societies stay auditable and stay under meaningful human control.

## References

- https://arxiv.org/abs/2308.08155
- https://github.com/microsoft/autogen
