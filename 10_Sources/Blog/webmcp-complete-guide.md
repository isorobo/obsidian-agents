---
type: source
status: draft
created: 2026-07-11
title: "WebMCP Tutorial: How Agents Use Websites as Tools"
authors:
- Jason Zhou
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 3.5
url: https://www.aibuilderclub.com/blog/webmcp-complete-guide
year: 2026
date_published: 2026-07-05
anthropic: false
topic:
- topic/mcp
tags:
- webmcp
- browser-agents
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
---

# WebMCP Tutorial: How Agents Use Websites as Tools

> Jason Zhou, "WebMCP Tutorial: How Agents Use Websites as Tools", AI Builder Club, Build AI Agents Course, 5 July 2026, https://www.aibuilderclub.com/blog/webmcp-complete-guide.

## Summary

Today's two ways an agent interacts with a website — brittle DOM-selector automation or slow, expensive screenshot-based computer use — both force the model to infer human intent from a page built for human eyes. WebMCP proposes a third path: the page itself registers typed, callable tools via `document.modelContext`, so the agent calls a declared function instead of guessing which pixel is the checkout button, running inside the user's own authenticated session rather than a separately replicated one.

## Key Concepts

- WebMCP exposes only MCP's tool vocabulary; the browser absorbs the transport and data layer that classic MCP handles with JSON-RPC and a server process.
- Tools execute in-page and reuse existing frontend code, sharing screen state live with the human user rather than running headless.
- Two registration paths: imperative (`document.modelContext.registerTool()` with a name, description, JSON Schema input, and an `execute` callback) or declarative (annotating standard HTML forms, from which the browser derives a tool automatically).
- As of the article's writing, WebMCP is a draft Community Group report co-edited by Microsoft and Google, shipping only as a Chrome origin trial; mainstream agents (Claude, ChatGPT, Gemini, Perplexity) do not yet call WebMCP tools on arbitrary sites.

## Terminology

- WebMCP — a JavaScript API letting a web page declare structured, MCP-style tools that an in-browser agent can discover and call, instead of scraping the rendered page.
- `exposedTo` — an origin allowlist controlling which cross-origin contexts may see a registered tool.
- `readOnlyHint` / `untrustedContentHint` — annotation flags marking a tool as non-mutating or its output as containing untrusted, potentially user-generated content.

## Architecture and Implementation

A registered tool carries a name, a model-read description, a JSON Schema `inputSchema`, an `execute` callback that runs in-page and calls existing frontend functions, an `AbortSignal` for unregistering on navigation, and optional `exposedTo` and annotation fields. At runtime the flow mirrors the six-step classic-MCP loop — discovery, model selection, argument emission, in-page execution, and result return — without requiring the page author to implement JSON-RPC directly. Getting started locally: enable the flag in Chrome 149-plus, install Google's Model Context Tool Inspector extension, test against Google's public demo apps, then register one tool behind a feature flag on a real site.

## Code Examples

A worked `document.modelContext.registerTool()` call registering an `add-todo` tool with a JSON Schema input and an `execute` callback that calls an existing frontend function and returns a text confirmation.

## Best Practices

- Inventory actions, not pages: identify the three to ten core verbs a site actually performs (search, filter, add-to-cart, book, subscribe) as the real tool candidates.
- Write tool descriptions with the same care as security documentation — the model reads them as decision points, not as marketing copy.
- Reuse existing validation and state-management code inside `execute` rather than duplicating logic; the lesson frames this as an architectural improvement independent of WebMCP adoption.
- Validate every tool input server-side regardless of client-side schema checks.

## Warnings and Anti-Patterns

- Tool names and descriptions are model-read and therefore a prompt-injection surface; a hostile page can embed instructions there exactly as a malicious MCP server can.
- Nothing verifies that a tool performs what its description claims — a tool named "check gift card balance" could execute arbitrary JavaScript, so descriptions must be treated as untrusted claims rather than guarantees.
- A tool that declares "helpful" extra input fields (email, address, current task) can be a deliberate over-parameterisation attack coaxing an agent into volunteering sensitive context.
- Because tools execute inside the user's authenticated session, a compromised agent acts with the user's own privileges — consequential actions need explicit user confirmation, not silent execution.

## Related Concepts

- [[mcp]]
- [[tool-use]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson frames adoption as genuinely uncertain — ROI depends on mainstream agents actually calling these tools, which had not happened as of publication — while arguing implementation cost is low enough that early adopters gain an edge if the market shifts toward tool-declaring sites.

## References

- WebMCP Tutorial: How Agents Use Websites as Tools — https://www.aibuilderclub.com/blog/webmcp-complete-guide
