---
type: source
status: draft
created: 2026-08-13
title: "How to Build an AI Agent from Scratch: A Step-by-Step Guide"
authors:
- Claude Code Playbooks
organisation: Claude Code Playbooks
source_type: blog
venue: Claude Code Playbooks Blog
url: TBD
year: 2026
date_published: 2026-04-14
anthropic: false
topic:
- topic/foundations
- topic/tool-use
tags:
- claude-code-playbooks
- agent-loop
- claude-md
- mcp
- parallel-agents
- tutorial
nlm_id:
nlm_skip: false
watchlist_channel:
authored_by: agens
---

# How to Build an AI Agent from Scratch: A Step-by-Step Guide

> Claude Code Playbooks, "How to Build an AI Agent from Scratch: A Step-by-Step Guide", Claude Code Playbooks Blog, 14 April 2026. URL TBD.

## Summary

A seven-step tutorial for a first agent, marked TUTORIAL and Intermediate, at a
14 minute read. The post opens with a working definition: an AI agent is an LLM
in a loop that uses tools, reads and writes memory, and decides what to do next.
The steps run in order: narrow the job, pick the model and the loop, add tools,
write the system prompt as `CLAUDE.md`, add memory, run agents in parallel, then
test and observe. The post closes by recommending three of the site's own
playbooks as templates. A site footer states: "Built for the Claude Code
community. Not affiliated with Anthropic."

## Key Concepts

- An agent is an LLM in a loop with tools, memory, and a next-action decision.
- Scope is the biggest predictor of success. A job that resists a one-sentence
  success criterion is too broad.
- Three items precede any code: the input, the output, and the boundary. The
  boundary lists what the agent must not do, such as send email, spend money, or
  delete files. The boundary keeps an autonomous loop safe.
- Tools separate a chatbot from an agent. An LLM without tools produces text
  alone.
- Everything above the loop, including memory, planning, and multi-agent
  orchestration, is a variation on the same pattern.

## Terminology

- Scratchpad memory: one Markdown file the agent reads at the start of a run
  and appends to at the end.
- Structured memory: a database or vector store the agent queries through
  tools.
- Fan-out / fan-in: split a task into independent subtasks, run them in
  parallel, merge the results.
- Critic loop: one agent proposes, a second critiques, the first revises.
- Eval set: a folder of sample inputs and expected outputs, re-run after every
  prompt change.

## Architecture and Implementation

The build runs in seven steps.

1. Define the job. The post contrasts "an agent that helps me manage my
   business" against "an agent that reads incoming invoice emails, extracts
   vendor, amount, and due date, and appends a row to a Google Sheet".
2. Pick the model and the loop. Claude Sonnet 4.6 is the 2026 default: fast,
   cheap enough to run in a loop, and strong at tool use. Opus covers deep
   reasoning over long context. Claude Code supplies the loop as a runtime, so
   the builder supplies tools and instructions alone.
3. Give the agent tools. Three routes rank by power: built-in tools
   (filesystem, bash, web fetch, shipped with Claude Code), custom functions
   described in JSON schema, and MCP servers. MCP is the standard for exposing
   tools to agents, and the post calls it the path that scales.
4. Write the system prompt in `CLAUDE.md` at the project root. Four sections:
   role, inputs and outputs, how to use the tools, and guardrails. The agent
   reads the file on every invocation.
5. Add memory. Start with scratchpad memory. Move to structured memory when
   memory outgrows the context window, or when several agents share state.
6. Run agents in parallel. Three patterns: fan-out / fan-in, specialist agents
   under a planner, and critic loops.
7. Test, observe, iterate. Log every tool call, run a fixed eval set, and gate
   irreversible actions.

## Code Examples

One pseudocode block, the agent loop:

```python
while not done:
    response = model.run(messages, tools=available_tools)
    if response.has_tool_call:
        result = execute_tool(response.tool_call)
        messages.append(result)
    else:
        done = True
return response.text
```

The post carries no other code. It points instead at three of its own
playbooks: AI Agent Builder, which scaffolds an agent from a plain-English
description; MCP Server Builder, which generates protocol handlers, schemas,
and an auth layer; and Parallel Task Agents, which splits a task across
concurrent sub-agents and merges the results.

## Best Practices

- State the success criterion in one sentence before writing code.
- Write the input, the output, and the boundary first.
- Default to Claude Sonnet 4.6 and reserve Opus for deep reasoning over long
  context.
- Move recurring explanations into `CLAUDE.md` rather than repeating them per
  run.
- Log every tool call: inputs, outputs, and the model's stated reasoning.
- Put irreversible actions behind human confirmation or a hard-coded allowlist.
- Treat `CLAUDE.md` as a living document. Every bug becomes a line in it.

## Warnings and Anti-Patterns

- Vague goals produce vague agents.
- Agents fail in ways deterministic programs do not: they hallucinate tool
  arguments, loop on one action, or misread the system prompt.
- A small prompt tweak regresses an edge case. The eval set catches it.
- Upgrading to structured memory before a concrete limit appears adds
  machinery most agents never need.
- The most ambitious agents lose to the narrow ones with clear boundaries and a
  prompt refined over a hundred runs.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[the-agent-loop]]
- [[tool-use]]
- [[mcp]]
- [[memory]]
- [[claude-code]]
- [[supervisor-worker-multi-agent]]
- [[prompt-engineering]]
- [[evaluation]]
- [[10_Sources/Blog/how-to-build-ai-agent-from-scratch|How to Build an AI Agent from Scratch in Python (AI Builder Club)]]
- [[10_Sources/Docs/claude-code-playbook-ai-agent-builder|AI Agent Builder playbook]]
- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]

## Future Work

The post frames the remaining work as iteration: tighten the prompt, add tools
as edge cases appear, and cut the tools the agent never calls. It leaves the
three playbooks as the recommended shortcut for a real project.

## References

- Claude Code Playbooks Blog, "How to Build an AI Agent from Scratch: A
  Step-by-Step Guide", 14 April 2026. URL TBD.
- Extract: `70_Research/_extracted/How to Build an AI Agent from Scratch_ A Step-by-Step Guide _ Claude Code Playbooks Blog.md`
