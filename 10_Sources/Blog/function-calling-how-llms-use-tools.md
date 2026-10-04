---
type: source
status: draft
created: 2026-07-11
title: "Function Calling Explained: How LLMs Actually Use Tools"
authors:
- Shirley
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 1.3
url: https://www.aibuilderclub.com/blog/function-calling-how-llms-use-tools
year: 2026
date_published: 2026-06-11
anthropic: false
topic:
- topic/tool-use
tags:
- function-calling
- json-schema
- course
nlm_id:
nlm_skip: false
watchlist_channel:
af_targets:
- af:ADR-0003
- af:ADR-0004
- af:RSCH-04/Q16
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: 28fe68f0c3456fa654630c97cdfd139cff94110beca5be800fd4ab27848b93b2
---

# Function Calling Explained: How LLMs Actually Use Tools

> Shirley, "Function Calling Explained: How LLMs Actually Use Tools", AI Builder Club, Build AI Agents Course, 11 June 2026, https://www.aibuilderclub.com/blog/function-calling-how-llms-use-tools.

## Summary

Before 2023, builders extracted tool calls by regex-parsing freeform model output, and JSON parse failures ran 15 to 25%. Native function calling replaced this with a three-step cycle — menu, order, serve — in which the model only ever decides what to request; application code executes it. Constrained decoding at inference time makes the model mathematically unable to emit a value outside the declared schema, which is why the failure rate collapsed to near zero.

## Key Concepts

- Function calling is a three-step cycle: the request declares a menu of tools (name, description, schema), the model orders by returning structured JSON, and the application serves the result by executing the tool.
- Constrained decoding, not just training, is what makes structured output reliable — invalid tokens are zeroed out at generation time.
- OpenAI, Anthropic, and Gemini share one architecture with different field names and result-message shapes.
- The `tool_choice` parameter controls calling behaviour: `auto`, `required`/`any`, a named tool, or `none`.

## Terminology

- Menu — the declared set of available tools, their names, descriptions, and parameter schemas, sent with the request.
- Order — the model's structured JSON output naming a tool and its arguments.
- Serve — the application's execution of the requested tool and return of its result to the model.
- Constrained decoding — an inference-time technique that zeroes out tokens that would violate the declared JSON schema.

## Architecture and Implementation

Tool schemas use JSON Schema with three fields carrying outsized weight on selection accuracy: `description` (functions as prompt engineering for tool selection), `enum` (locks a parameter to fixed values, preventing casing drift such as "celsius" vs "Celsius"), and `required` (marks mandatory parameters; everything else is optional). Schemas should stay shallow — past three nesting levels, argument accuracy visibly degrades. Errors should be fed back to the model with actionable context rather than a generic failure string, with a retry limit of two to three attempts and a clear split between recoverable and unrecoverable failures.

## Code Examples

The lesson does not provide a full runnable program; it walks schema-writing patterns and the shape of request and result payloads across OpenAI, Anthropic, and Gemini.

## Best Practices

- Write tool descriptions as when-to-use guidance with boundary conditions against similar tools, not a restatement of the function's mechanism.
- Cap parameters at five to eight per tool; deeper interfaces raise argument errors.
- Lock enumerable values with `enum` rather than free strings.
- Embed examples in parameter descriptions, for example `"e.g. 'Tokyo', 'New York'"`.
- Choose descriptive tool names — `search_code_by_regex` outperforms `search`.
- Force a named tool via `tool_choice` for reliable structured-data extraction tasks.

## Warnings and Anti-Patterns

- Pre-2023 regex parsing of freeform output produced 15 to 25% JSON parse failures and invented tool names.
- Nesting a schema past three levels measurably degrades argument accuracy.
- Returning a bare "failed" string denies the model the context it needs to self-correct.

## Related Concepts

- [[tool-use]]
- [[the-agent-loop]]
- [[mcp]]
- [[claude-code]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson positions function calling as the base layer beneath the agent loop, MCP-based tool distribution, and Claude Code's refined tooling, without expanding on any of the three in this piece.

## References

- Function Calling Explained: How LLMs Actually Use Tools — https://www.aibuilderclub.com/blog/function-calling-how-llms-use-tools
