---
type: source
status: draft
created: 2026-07-11
title: "MCP Builder - Claude Skill for Building MCP Servers"
authors:
- Anthropic
organisation: claudeskills.org (mirrors anthropics/skills, Anthropic)
source_type: docs
venue: claudeskills.org
url: https://www.claudeskills.org/docs/skills-cases/mcp-builder
year: 2026
date_published: 2026-04-20
anthropic: true
topic:
- topic/mcp
- topic/agent-skills
tags:
- mcp
- agent-skills
- fastmcp
nlm_id:
nlm_skip: false
watchlist_channel:
---

# MCP Builder - Claude Skill for Building MCP Servers

> Anthropic, "MCP Builder - Claude Skill for Building MCP Servers", claudeskills.org (content adapted from `anthropics/skills`, MIT licence), last synced 8 July 2026 against the 20 April 2026 upstream, https://www.claudeskills.org/docs/skills-cases/mcp-builder.

## Summary

An official Anthropic Agent Skill that turns Claude into a guided builder of MCP servers, covering both Python (FastMCP) and Node/TypeScript (the MCP SDK). Rather than a single prompt, the skill packages design guidelines, per-language implementation references, and an evaluation harness, so a server Claude builds with it is scaffolded, reviewed, and tested, not just generated. It is the practical, hands-on counterpart to this vault's existing conceptual MCP lessons — [[10_Sources/Blog/mcp-101-build-your-first-server|MCP 101]] teaches what MCP is and builds one server by hand; this skill is what Claude itself uses to build one on request.

## Key Concepts

- Development runs in three structured phases: research and planning (studying MCP design patterns and the target framework), implementation (project structure, core infrastructure, then individual tools with explicit input/output/error handling), and review and test (a code-quality pass plus agent-facing evaluations, not unit tests alone).
- Evaluation is treated as a first-class deliverable, not an afterthought — the skill folder ships an evaluation harness with example scripts alongside the design guidance.
- Language-specific documentation (Python and Node.js implementation references) is kept in separate files rather than one combined document, for maintainability and faster on-demand loading — a direct instance of the progressive-disclosure principle already documented in [[10_Sources/Blog/agent-skills-best-practices|the Anthropic Skills playbook]].

## Terminology

- Agent-facing evaluation — testing an MCP server the way an agent actually uses it (tool selection, argument correctness, error recovery), distinct from conventional unit testing of the server's code.

## Architecture and Implementation

The skill folder holds design guidelines, per-language implementation references (Python via FastMCP, Node/TypeScript via the official MCP SDK), an evaluation harness with example scripts, and connection utilities — the same folder-plus-reference-subfolder shape this vault's Agent Skills sources describe generally, applied here to one specific, high-value skill.

## Code Examples

None reproduced in the fetched summary; the skill folder itself ships example evaluation scripts and per-language implementation references, not shown in full here.

## Best Practices

- Treat evaluation as part of the deliverable a skill produces, not a separate, optional step.
- Split language-specific reference material into distinct files rather than one large combined document.
- Follow the three-phase structure (research, implementation, review/test) rather than jumping straight to code.

## Warnings and Anti-Patterns

None stated in the content retrieved.

## Related Concepts

- [[mcp]]
- [[10_Sources/Blog/mcp-101-build-your-first-server|MCP 101: Build Your First MCP Server]]
- [[10_Sources/Blog/agent-skills-best-practices|Anthropic's 300+ Claude Code Skills: Lessons Learned]]

## Future Work

The fetched page gives a summary rather than the full `SKILL.md` and its evaluation scripts; a deeper pass reading the actual `anthropics/skills` repository directly would surface the concrete design-guideline and evaluation-harness content this summary only describes at a high level.

## References

- MCP Builder - Claude Skill for Building MCP Servers — https://www.claudeskills.org/docs/skills-cases/mcp-builder
- Upstream source: `anthropics/skills` (MIT licence)
