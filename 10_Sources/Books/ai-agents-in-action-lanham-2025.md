---
type: source
status: draft
created: 2026-08-13
title: "AI Agents in Action"
authors:
- Micheal Lanham
organisation: Manning Publications
source_type: book
venue: Manning Publications
url: https://www.manning.com/books/ai-agents-in-action
year: 2025
date_published: 
anthropic: false
topic:
- topic/foundations
- topic/agent-patterns
tags: [autogen, crewai, semantic-kernel, behaviour-trees, prompt-flow, rag]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
af_targets:
- af:ADR-0001
- af:RSCH-04/Q01
- af:RSCH-04/Q11
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: a36deb558616e01f91992a55af4ba75df879a44d7dba31f86e3ce6a0b701a70c
---

# AI Agents in Action

> Full citation: Lanham, M. "AI Agents in Action." Manning Publications, Shelter Island, 2025. ISBN 9781633436343.

## Summary

Micheal Lanham teaches agent construction through working code. The book runs
11 chapters and two appendices. Chapter 1 defines the agent and names its five
component systems. Chapters 2 and 3 cover the OpenAI API, local models through
LM Studio, prompt engineering, and the GPT Assistants platform. Chapter 4
builds multi-agent systems on AutoGen and CrewAI. Chapter 5 gives agents
actions through OpenAI functions and Microsoft Semantic Kernel. Chapter 6
borrows the behaviour tree from robotics and games, then extends it into the
agentic behaviour tree. Chapter 7 assembles Nexus, the author's open source
agent platform. Chapter 8 covers retrieval, knowledge, and memory. Chapter 9
applies Microsoft prompt flow to prompt evaluation. Chapters 10 and 11 close
on reasoning, evaluation, planning, and feedback. The book assumes basic
Python and no prior agent experience. Each chapter ends with exercises.

## Key Concepts

- Four interaction cases: direct user interaction, agent proxy, agent acting
  with user approval, and autonomous agent.
- Five component systems of a single agent: profile and persona, actions and
  tool use, memory and knowledge, reasoning and evaluation, planning and
  feedback.
- Multi-agent systems as agent profiles working under a controller or proxy,
  shown through a coder and tester pair.
- Behaviour trees as a control layer for assistants, with selector, sequence,
  condition, action, decorator, and parallel nodes.
- Agentic behaviour trees, where prompts drive the action and condition nodes
  and the LLM supplies the decision.
- Retrieval as two distinct stores: knowledge from ingested documents, memory
  from past interactions.
- Systemic prompt engineering, where a rubric scores a profile and batch runs
  compare variants.
- Reasoning techniques: few-shot, zero-shot, chain of thought, prompt
  chaining, self-consistency, and tree of thought.
- Planning as the skill that separates an agent from a chatbot, split into
  sequential and parallel action planning.

## Terminology

- **AI interface** - a set of functions, tools, and data layers that expose
  data and applications through natural language.
- **Agent profile** - the combined prompt elements that define an agent's
  role, tools, knowledge, memory, reasoning, and planning.
- **Semantic function** - a Semantic Kernel unit that wraps a prompt template.
- **Native function** - a Semantic Kernel unit that wraps code calling an API
  or other interface.
- **Agentic behaviour tree (ABT)** - a behaviour tree whose nodes delegate
  conditions and actions to assistants.
- **Back chaining** - building a behaviour tree backward from the goal
  behaviour to the actions and conditions it requires.
- **Grounding** - the score a profile earns against a stated rubric.
- **Semantic memory augmentation** - separating semantic, episodic, and
  procedural memory and injecting each by type.
- **Memory compression** - condensing stored memory and knowledge through
  clustering and summarisation.

## Architecture and Implementation

The five component systems form the architecture spine of the whole book. Each
later chapter builds one component and returns it to the same skeleton. Chapter
7 assembles the parts into Nexus, an open source platform with a Streamlit chat
front end, an agent engine, profile storage, and pluggable actions. Chapter 8
adds knowledge stores and memory stores to Nexus, with Chroma behind the vector
search. Chapter 11 adds a custom planner to a Nexus agent and contrasts it with
a raw LLM.

Chapter 6 supplies a second architecture. The GPT Assistants Playground is a
Gradio application that mirrors the OpenAI Assistants Playground and adds
custom actions, an assistants database, and local code execution. A behaviour
tree built with `py_trees` sits above the assistants and controls them. The
book applies the pattern to a coding challenge and to posting videos to X.

Chapter 5 sets out the Semantic Kernel layering rule. A semantic function may
call another semantic function or a native function, so prompts and code nest
as execution stages. Chapter 9 defines the evaluation architecture: a
generative flow runs first, an evaluation flow scores and aggregates after it,
and the Visualize Runs view compares aggregated rubric scores across variants.

## Code Examples

The code lives in three public GitHub repositories under the author's account:
`GPTAgents` for the chapter examples, `GPTAssistantsPlayground` for the
assistant platform, and `Nexus` for the agent platform. Listings run in Python
and follow a low-code approach.

The frameworks and services the book teaches:

- OpenAI chat completions API, function calling, and the GPT Assistants
  platform with Code Interpreter and file uploads.
- LM Studio for downloading, running, and serving open source models locally.
- AutoGen and AutoGen Studio for conversational multi-agent systems, skills,
  group chat, and the response cache.
- CrewAI for role-based crews, sequential and hierarchical task management,
  and AgentOps for observability and cost tracking.
- Microsoft Semantic Kernel for semantic and native functions, plugins, and a
  semantic service layer over API calls.
- `py_trees` for behaviour trees, and Gradio for the Playground interface.
- LangChain for document loading, token splitting, vector stores, and short
  and long term conversation memory.
- Chroma for embedding storage and similarity search, alongside a from
  scratch TF-IDF and cosine similarity walkthrough.
- Microsoft prompt flow for profile variants, Jinja2 profile templates, batch
  runs, evaluation flows, and a deployed flow API.
- Streamlit for the Nexus chat and streaming chat interface.

Appendix A covers OpenAI and Azure OpenAI account setup, API keys, and
deployments. Appendix B covers the Python development environment. The author
puts the total API cost of the exercises under US$100.

## Best Practices

- Limit an agent to the actions it needs for the task.
- Score a profile against a written rubric before shipping it.
- Iterate prompts through batch runs and compare variants on the same data.
- Build a behaviour tree by back chaining from the goal behaviour.
- Keep knowledge stores and memory stores separate, then select memory by type.
- Compress stored memory through clustering and summarisation to hold context
  cost down.
- Add an observability tool such as AgentOps once agent interactions multiply.
- Pair a coder agent with a critic or tester agent to cut errors.
- Keep the API key on the development machine, inside an `.env` file.

## Warnings and Anti-Patterns

Too many actions overwhelm an agent and invite misuse of tools it never needed.
Prompt engineering alone reaches a ceiling, which is the gap agent systems
fill. Autonomous agents carry the sharpest ethical and safety risk, since they
plan, decide, and act without approval at each step. The book ties adoption to
trust in three things: the decision process, the guardrail and evaluation
system, and the goal definition. Most production-ready agent tools stop short
of full autonomy for that reason. Only advanced models handle sequential
planning, so a weaker model produces a plan it cannot execute.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[agent-vs-llm]]
- [[workflow-vs-autonomous-agent]]
- [[the-agent-loop]]
- [[tool-use]]
- [[memory]]
- [[retrieval-augmented-generation]]
- [[planning-and-reasoning]]
- [[plan-and-execute]]
- [[prompt-engineering]]
- [[evaluation]]
- [[supervisor-worker-multi-agent]]

## Future Work

Lanham forecasts that reasoning, planning, evaluation, and feedback move inside
the model itself. He points to OpenAI Strawberry as the first step. He predicts
that natural language AI interfaces displace user interfaces, APIs, and SQL for
many use cases. He notes the view that autonomous agent systems form a path to
artificial general intelligence, without endorsing a date. Nexus carries a
roadmap toward an API and a Discord bot alongside the web interface.

## References

- Manning book page: https://www.manning.com/books/ai-agents-in-action
- liveBook edition: https://livebook.manning.com/book/ai-agents-in-action
- GPT-Agents repository: https://github.com/cxbxmxcx/GPTAgents
- GPT Assistants Playground: https://github.com/cxbxmxcx/GPTAssistantsPlayground
- Nexus: https://github.com/cxbxmxcx/Nexus
- Rodney A. Brooks, credited in Chapter 6 for the behaviour tree in robotics.

## See also

- [[10_Sources/Books/agentic-design-patterns-gulli-2025|Agentic Design Patterns]]
- [[10_Sources/Books/ai-agents-illustrated-guidebook-chawla-pachaar-2025|AI Agents Illustrated Guidebook]]
- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]
- [[agent-patterns-index]]
