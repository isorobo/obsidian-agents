---
type: concept
status: draft
created: 2026-07-10
name: Tool Use
slug: tool-use
topic:
- topic/tool-use
- topic/foundations
tags:
- tools
- function-calling
- agents
synonyms:
- function calling
- tool calling
- tool invocation
defined_in: "[[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]"
related_concepts:
- "[[the-agent-loop]]"
- "[[what-is-an-ai-agent]]"
- "[[mcp]]"
af_targets:
- af:ADR-0004
- af:RSCH-04/Q06
- af:RSCH-04/Q16
wiki_indexed: '2026-10-04T03:42:35Z'
wiki_hash: 350bf0ddfd2818bf1a43da35f560ec3534a9caae38faaf997f1708ef775a5164
---

# Tool Use

> Tool use is the mechanism by which a model calls an external function, receives the result, and folds it back into its reasoning.

## Summary

Tool use gives a model hands. The developer defines a tool with a name, a description, and a typed input schema. The model reads the definitions and emits a tool call when it needs one. The harness runs the tool and returns the result to the model. This loop lets a model fetch data, run code, and change state in the world. Tool use is the primitive that separates a talking model from an acting agent.

## Key Concepts

- A tool has a name, a description, and a typed input schema.
- The model emits a tool call; the harness runs it and returns the result.
- Clear tool definitions drive correct tool selection.
- The Model Context Protocol standardises how tools reach the model.

## Detail

A tool definition is a contract. The name states the action. The description states what the tool does and when to use it. The schema types each input. The model reads these fields and decides whether to call the tool. A vague description causes a wrong call. Anthropic advises tool design as care equal to prompt design.

The call runs outside the model. The harness executes the function, then returns a result block. The model reads the result and continues the loop. The Model Context Protocol gives tools an open standard. One protocol lets many servers expose tools to many agents without bespoke glue.

## Trade-offs and Limits

Tools extend a model past text into live data and action. They also widen the attack surface and the failure set. A malformed schema or a slow tool breaks the loop. Too many tools crowd the context and confuse selection. A small, sharp tool set beats a large, vague one.

## Related

- [[the-agent-loop]]
- [[what-is-an-ai-agent]]
- [[mcp]]
- [[agent-vs-llm]]

## Sources

- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]
- Writing effective tools for AI agents — https://www.anthropic.com/engineering/writing-tools-for-agents
- What is the Model Context Protocol — https://docs.anthropic.com/en/docs/agents-and-tools/mcp
- [[10_Sources/Blog/anthropic-how-we-contain-claude|How we contain Claude across products]]
- [[10_Sources/Blog/agent-modes-plan-default-auto|Plan vs Default vs Auto Mode]]
- [[10_Sources/Blog/agent-sandbox-os-level-security|Agent Sandboxes: OS-Level Security]]
- [[10_Sources/Blog/anthropic-claude-code-auto-mode|How we built Claude Code auto mode]]
- [[10_Sources/Blog/anthropic-eval-awareness-browsecomp|Eval awareness in BrowseComp]]
- [[10_Sources/Docs/claude-agent-sdk-hooks|Agent SDK hooks]]
- [[10_Sources/Docs/claude-agent-sdk-permissions|Agent SDK permissions]]
- [[10_Sources/Docs/claude-code-headless-mode|Run Claude Code programmatically]]
- [[10_Sources/Docs/claude-code-hooks-reference|Claude Code hooks reference]]
- [[10_Sources/Docs/claude-code-permissions|Claude Code permissions]]
- [[10_Sources/Papers/mid-harness-kang-2026|Mid-Harness (Kang et al., 2026)]]
- [[10_Sources/Papers/swe-agent-computer-interfaces-yang-2024|SWE-agent (Yang et al., 2024)]]
- [[10_Sources/Release-Notes/claude-fable-5-1-2026-09-01|Claude Fable 5.1]]
- [[10_Sources/Release-Notes/claude-opus-5-5-2026-09-22|Claude Opus 5.5]]
- [[10_Sources/Release-Notes/claude-sonnet-5-5-2026-09-28|Claude Sonnet 5.5]]
- [[10_Sources/Repos/12-factor-agents|12-Factor Agents]]
- [[10_Sources/Repos/anthropic-skills-repository|Anthropic Agent Skills Repository]]
- [[10_Sources/Repos/claude-agent-sdk-python|Claude Agent SDK for Python]]
- [[10_Sources/Repos/commerce-agents|Claude Commerce Agents]]
- [[10_Sources/Repos/learn-agent-architecture|learn-agent-architecture]]
- [[10_Sources/Repos/mini-swe-agent|mini-SWE-agent]]
- [[10_Sources/Repos/sandbox-runtime|Anthropic Sandbox Runtime]]
- [[10_Sources/Repos/smolagents|smolagents]]

## See also

- [[MOC - Tool Use]]
