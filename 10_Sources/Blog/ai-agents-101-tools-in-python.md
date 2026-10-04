---
type: source
status: draft
created: 2026-07-11
title: "AI Agent Tools in Python (AI Agents 101, Part 2)"
authors:
- AI Builder Club
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 1.4
url: https://www.aibuilderclub.com/blog/ai-agents-101-part-2
year: 2026
date_published: 2026-04-14
anthropic: false
topic:
- topic/tool-use
tags:
- tools
- error-handling
- course
nlm_id:
nlm_skip: false
watchlist_channel:
af_targets:
- af:ADR-0004
- af:BI-11
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 9b9f6a27337f711afcca23d547aad3ab3f2fbc63131f0e9cd69a397a1e7d20aa
---

# AI Agent Tools in Python (AI Agents 101, Part 2)

> AI Builder Club, "AI Agent Tools in Python (AI Agents 101, Part 2)", Build AI Agents Course, 14 April 2026 (updated 11 June 2026), https://www.aibuilderclub.com/blog/ai-agents-101-part-2.

## Summary

Part 2 extends the Part 1 agent, which could only list and read local files and crashed on any tool failure, with three new tools — web search, code execution, and file writing — and a resilience layer the series calls "the part most tutorials skip". The lesson treats error recovery as a first-class design problem: every tool returns structured errors with a `retry` flag rather than opaque strings, so the model itself can decide whether to retry.

## Key Concepts

- Structured error responses (JSON with a `retry` flag and a suggestion) let the model decide whether to reattempt, instead of hard-coding retry logic.
- Path traversal defence requires `pathlib.Path.is_relative_to()`; naive `startswith()` prefix checks pass a sibling directory like `/project-evil` against a root of `/project`.
- Code execution via `subprocess` to a temp file is acceptable for local development; production requires sandboxing (E2B, Modal, or Docker).
- Tool count has a measured accuracy ceiling: roughly ten tools hold 95%+ selection accuracy, thirty drop to about 85%, and beyond fifty requires deferred loading or tool splitting.

## Terminology

- Tool registry — a dictionary mapping tool names to their implementation functions and JSON schemas.
- Path traversal — an attack where a relative path string such as `../../../etc/passwd` escapes an intended directory boundary.
- Transient failure — a temporary error, such as a network hiccup or brief rate limit, that may succeed on retry.

## Architecture and Implementation

The web-search tool wraps the Tavily API with an explicit `timeout=10`, truncates result snippets to 300 characters to bound token cost, and differentiates retriable errors (HTTP 429) from non-retriable ones. The code-execution tool writes untrusted code to a temporary file rather than calling `eval()` or `exec()` directly, enforces a 30-second timeout, captures stdout and stderr, and cleans up the temp file in a `finally` block. The write-file tool resolves and checks every path with `pathlib.Path.resolve()` and `.is_relative_to()` before writing, and creates parent directories as needed. The updated agent loop wraps tool execution in `try/except`, returning `{"error": ..., "retry": false}` instead of letting an exception crash the loop, and a system-prompt instruction tells the model to report failure clearly after two consecutive failures on the same task rather than looping.

## Code Examples

Full implementations are given for the web-search, code-execution, and write-file tools, an exponential-backoff retry wrapper (1s, 2s waits, retrying only when `retry: true`), and the revised agent loop with exception handling. Three graded exercises follow: a research-and-persist task, a code-verified compound-interest calculation, and an intentional API-key failure to observe degradation.

## Best Practices

- Put a timeout on every external call without exception.
- Return structured errors with retry hints, never opaque strings.
- Clean up temporary files in a `finally` block.
- Wrap all tool execution in exception handling so a single bad call cannot crash the loop.
- Cap output length on every tool — 300 characters for search snippets, 2000 for code output.
- Sandbox code execution (E2B, Modal, Docker) before any production deployment.

## Warnings and Anti-Patterns

- `eval()` or `exec()` on untrusted strings is unsafe at any stage; write to a temp file and execute as a subprocess instead.
- String-prefix path checks (`startswith()`) are a security bug, not a shortcut; a directory named `/project-evil` passes a naive check against `/project`.
- Uncapped tool output silently drives up token cost as message history accumulates.
- Subprocess startup adds 200 to 400ms per call, which is fine interactively but a bottleneck in a tight loop.

## Related Concepts

- [[tool-use]]
- [[the-agent-loop]]
- [[mcp]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The series continues into memory systems (Part 3), multi-agent orchestration (Part 4), and production deployment (Part 5).

## References

- AI Agent Tools in Python (AI Agents 101, Part 2) — https://www.aibuilderclub.com/blog/ai-agents-101-part-2
