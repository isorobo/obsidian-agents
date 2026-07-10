---
type: guide
status: draft
created: 2026-07-10
name: Choosing a Layer in the Claude Agent Stack
slug: choosing-a-layer-in-the-claude-agent-stack
topic:
- topic/claude-sdk
- topic/claude-code
tags: [claude-agent-sdk, claude-code, langflow, tooling-choice]
synonyms: []
related_concepts:
- "[[claude-agent-sdk]]"
- "[[claude-code]]"
- "[[mcp]]"
---

# Choosing a Layer in the Claude Agent Stack

> Pick a visual canvas for a first build, the Claude Agent SDK for production logic, and Claude Code for personal automation.

## Goal

Anthropic ships no drag-and-drop canvas. The stack is code-first and
text-first. This guide sets a rule for the reader's next build: pick the
layer the job needs, not the tool already open. It stops the default reflex
of reaching for whichever surface is familiar.

## Prerequisites

- Familiarity with [[what-is-an-ai-agent]].
- Familiarity with [[mcp]], the contract that carries tools across layers.

## Steps

1. **Name the build's audience and lifespan.** A prototype shown to a
   non-coder differs from a production agent that ships. The answer picks
   the layer.

2. **Choose the visual canvas for first builds and demos.** Use Langflow or
   LangGraph Studio, both pointing at the Anthropic API. Drop an Anthropic
   node, paste an API key, drag tools onto the canvas, ship. Reach for this
   layer on a first build, a prototype, or anything a non-coder must see and
   understand.

3. **Choose the Claude Agent SDK for production agents.** Install it in
   Python or TypeScript. It is the official agent loop: tool use, sub-agents,
   memory, and streaming. Reach for this layer for production agents, custom
   logic, and anything the canvas cannot express. A small agent runs in 50 to
   100 lines once the docs are read once.

4. **Choose Claude Code for personal automation.** Use subagents, skills,
   slash commands, and hooks, triggered from a terminal. Reach for this layer
   for workflows the reader runs personally, not workflows shipped to
   others.

5. **Check portability before committing.** All three layers speak Anthropic
   models, and none lock the reader to a single vendor. Langflow and
   LangGraph swap providers from a dropdown. The Agent SDK swaps with one
   config line. Claude Code stays Anthropic, but its artefacts are plain
   markdown, so the prompt library survives a tool change.

6. **Move up a layer only when the canvas breaks.** Prototype on Langflow.
   Ship through the SDK once the design holds. Move a Langflow build to
   LangGraph Studio once it needs branching, retries, or parallel
   sub-agents.

## Code

This is a decision guide, not a code walkthrough. For implementation, read
the Claude Agent SDK docs and build the smallest possible agent first: one
tool, one prompt, one task.

## Verification

The reader has picked the right layer when they can state, in one sentence
each, why the chosen layer beats the other two for this specific build.

- State why a visual canvas beats the SDK and Claude Code for this build, or
  why it does not.
- State why the SDK beats a canvas and Claude Code for this build, or why it
  does not.
- State why Claude Code beats a canvas and the SDK for this build, or why it
  does not.

A reader who cannot state the reason has defaulted to a familiar tool
instead of choosing a layer.

## Common Pitfalls

- Treating the canvas as a runtime instead of a thinking tool. A canvas ages
  badly under version control. Prototype on it, then ship through the SDK.
- Skipping the prompt file. An agent prompt written only inside a canvas has
  no asset once the canvas changes. Write every agent prompt to a markdown
  file, checked into git.
- Reaching for n8n for agent reasoning. Keep n8n for business plumbing, such
  as CRM writes, email sends, and scheduled triggers. Let Claude do the
  reasoning; let n8n move the data.

## Related

- [[claude-agent-sdk]]
- [[claude-code]]
- [[mcp]]
- [[what-is-an-ai-agent]]

## Sources

- Simon's own working notes on the Anthropic agent stack, 2026.

## See also

- [[MOC - Claude SDK]]
- [[MOC - Claude Code]]
