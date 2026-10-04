---
type: guide
status: draft
created: 2026-07-11
name: "AI Agents Course — Chapters 2 & 3: From Scratch to Infrastructure (Synthesis)"
slug: ai-agents-course-chapters-2-3
topic:
- topic/tool-use
tags: [ai-builder-club, course-notes, mcp, multi-agent, memory, context-engineering, prompt-engineering, agent-skills]
synonyms: ["AI Builder Club Chapters 2-3", "Build AI Agents Course — Build From Scratch & Tools and Infrastructure"]
related_concepts:
- "[[what-is-an-ai-agent]]"
- "[[the-agent-loop]]"
- "[[tool-use]]"
- "[[memory]]"
- "[[supervisor-worker-multi-agent]]"
- "[[mcp]]"
- "[[claude-code]]"
- "[[prompt-engineering]]"
af_targets:
- af:DELEG-02
- af:RSCH-04/Q24
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: dd63f046798da09d30e99c442842cf2aa1cfcde23fc78d6bfba76f6fe64e716e
---

# AI Agents Course — Chapters 2 & 3: From Scratch to Infrastructure (Synthesis)

> A single, synthesised map of AI Builder Club's "Build AI Agents Course" Chapter 2 (Build From Scratch, 2.1–2.4) and Chapter 3 (Tools & Infrastructure, 3.1–3.13) — seventeen lessons compressed into one reading.

## Goal

Chapter 1 established the four-component agent (brain, tools, memory, loop).
This guide covers what the course builds on top of that base: a from-scratch
agent and a from-scratch multi-agent system in plain Python (Chapter 2), then
the full infrastructure layer an agent needs in production — MCP, context
engineering, retrieval, prompt discipline, and the emerging Agent Skills
ecosystem (Chapter 3). A reader finishes able to explain not just what each
piece is, but the specific trade-off it buys and the point at which it earns
its complexity.

One correction before the map: the course index labels lesson 3.4 "Why MCP is
Dead & Skills Replace It", but the article actually published at that URL is
Anthropic's internal Claude Code Skills playbook — a related topic, not the
MCP-obsolescence argument the title promises. This guide follows the article
as published, not the index's title.

## Prerequisites

- [[10_Sources/Blog/how-to-build-ai-agent-from-scratch|Chapter 1's agent loop and tool-use lessons]],
  or equivalent comfort with the brain/tools/memory/loop model.
- Comfort reading Python; every Chapter 2 code pattern assumes it.

## Steps

### Part One: Build From Scratch (2.1 – 2.4)

**2.1 — A 60-line agent, rebuilt.** The same three primitives from Chapter 1
— a tool-capable LLM, a tool registry, a loop — rebuilt as a self-contained
exercise, with memory, planning, and reflection explicitly named as later
additions on top, not separate primitives. The lesson's stronger claim: most
production agents the authors have seen run on hand-written loops, not
frameworks, so understanding the loop is not a stepping stone to a framework —
it may be the whole job.

**2.2 — Coordinator/worker, 200 lines.** A concrete research-and-write system
(researcher, writer, fact-checker) built the same way — plain Python, not a
framework. The discipline that matters most: multi-agent systems cost three
to eight times more than a single agent, so the decision to split into
multiple agents needs a *measured* justification — genuine role
specialisation, conflicting prompts, or real parallel speed-up — not a
default preference for the more sophisticated-looking architecture. "Boring
is good": explicit Python handoffs beat free-form agent-to-agent
conversation, which the lesson ties directly to looping and hallucination.

**2.3 — Hermes: persistent, self-hosted, self-improving.** A case study in
what a session-based tool cannot do alone: Nous Research's Hermes persists
memory across sessions on a three-tier model, runs scheduled background work
while the user is offline, and encodes its own repeated multi-step tasks as
local skill files — explicitly flagged as drafts needing human review, not
autonomous production code. Framed as complementary to, not competing with,
session-based coding agents.

**2.4 — Local deployment has arrived.** Google DeepMind's Gemma 4 (four
variants, 2.3B to 31B parameters, Apache 2.0, native function calling) makes
fully local agent deployment a legitimate default for a specific list of
cases — data that cannot leave infrastructure, per-token cost pressure,
offline requirements, latency sensitivity — not merely a fallback when cloud
access is unavailable. Cloud APIs still win on best-in-class reasoning and
large-scale multi-agent coordination.

### Part Two: MCP Fundamentals (3.1 – 3.3)

**3.1 — What MCP is and a first server.** MCP standardises what function
calling could not: one open protocol (three primitives — Tools, Resources,
Prompts — over JSON-RPC) that any client can speak and any server can
implement, instead of a bespoke integration per API. A roughly 60-line Python
weather server, wired into Claude Desktop and Cursor by JSON config, is the
worked example.

**3.2 — What actually happens underneath.** An MCP config is a shell command
disassembled into JSON; the client spawns the server as an ordinary local
process — no different in kind from anything else launched from a shell.
STDIO (local, secured by process isolation, not authentication) and SSE
(remote, HTTP-based, needs real auth) carry the same JSON-RPC messages either
way. The entire agentic loop, at the protocol level, is six repeating steps
and nothing else — a claim worth holding onto through every later lesson that
adds apparent complexity on top.

**3.3 — Six ways a server turns hostile.** Because tool descriptions are
model-visible prompts, not just human documentation, MCP's trust model
differs from ordinary supply-chain risk. Six named vectors: description
poisoning, data exfiltration, malicious command execution, sensitive file
reads, rug pulls (a clean version turning malicious later), and cross-server
tool hijacking, where trust across installed servers is multiplicative, not
additive — five clean servers plus one compromised one is not "five-sixths
safe." A five-step, roughly fifteen-minute audit (descriptions, network
calls, shell calls, file access, install-time scripts) closes the lesson.

### Part Three: Skills and Web Agents (3.4 – 3.5)

**3.4 — Anthropic's Skills playbook.** A Skill is a folder — instructions,
scripts, and reference material together — not a single Markdown file; the
folder itself is the context-engineering surface. Nine functional types exist
(verification Skills deliver, per Anthropic, the largest quality gain);
progressive disclosure keeps always-needed instructions in `SKILL.md` and
defers detail to `references/`; and a Skill's description functions as a
trigger signal read by the model, not documentation for a person — the
single most common reason a Skill goes unused is a description written for a
human instead of as a match against how a user actually phrases a request.

**3.5 — WebMCP: the page as the tool provider.** Where DOM scraping and
computer use both force a model to infer intent from a human-facing page,
WebMCP lets the page itself register typed, callable tools via
`document.modelContext`, executing in-page inside the user's own
authenticated session. Still a draft spec shipping only as a Chrome origin
trial at time of writing, with no mainstream agent yet calling WebMCP tools
on arbitrary sites — genuinely uncertain adoption, low implementation cost.
Security concerns mirror 3.3's almost exactly: tool descriptions are a
prompt-injection surface here too, and nothing verifies a tool does what its
description claims.

### Part Four: Context and Knowledge (3.6 – 3.9)

**3.6 — Context engineering: the real bottleneck.** Production agents run
roughly a hundred input tokens per output token, so context quality — not
model quality — usually governs agent quality. The LLM-as-CPU,
context-window-as-RAM frame organises four failure modes (poisoning,
distraction, confusion, clash) against four management strategies
(offloading, just-in-time retrieval, isolation, compression), plus a
KV-cache layer underneath all of it: freeze the prefix, keep history
append-only, mask rather than remove tools, since a single volatile token
(a live timestamp is the canonical mistake) silently destroys a roughly
ten-times cache-cost saving.

**3.7 — RAG versus long context versus fine-tuning.** Three ways to give a
model working knowledge it was not trained on, chosen by a decision table
rather than a universal winner: small static corpora stay in context, large
or changing corpora needing citations go through RAG, and changing the
model's behaviour or style is what fine-tuning is actually for. The modern
RAG pipeline is chunking (the single highest-leverage decision), hybrid
retrieval, reranking, and grounded assembly — with agentic retrieval (search
as a tool the model wields itself, as Claude Code does with grep) displacing
the fixed 2023-style chunk-and-embed pattern on messy document sets.

**3.8 — Fixing coding-agent memory loss.** `agentmemory`, an MCP server
built for exactly the coding-agent use case, captures activity through
lifecycle hooks, compresses it into structured facts across the same four-
tier taxonomy as Chapter 1's memory lesson (working, episodic, semantic,
procedural), and injects only what is relevant — roughly 1,900 tokens per
session against a stated 95.2% top-five recall. It complements rather than
replaces a trimmed `CLAUDE.md`: static rules stay in the file; everything
that accumulates goes through the dynamic memory layer.

**3.9 — Prompt engineering, structured.** One mental model carries the
lesson: the Door Rule — the model only knows what is in the context window,
so most prompt failures are missing-context failures, not reasoning
failures. A well-formed prompt has four parts (role, task, context, output
format); chain-of-thought, few-shot examples, negative instructions, and
constrained output are the four techniques that consistently move quality;
and model tier should match task complexity, not default to the most capable
option available.

### Part Five: The Agent Skills Ecosystem and Codebase Memory (3.10 – 3.13)

**3.10 — MarkItDown: clean input for the pipeline.** Microsoft's
structure-preserving document converter (PDFs, Office files, and more, into
Markdown that keeps headings as headings and tables as tables) typically cuts
downstream token usage 30 to 50% against raw extracted text, at the cost of
top-end table-extraction accuracy against specialised competitors. The
production rule worth keeping: expose only `convert_local()` or
`convert_stream()` in a user-facing application, never the bare `convert()`,
which accepts arbitrary remote URIs.

**3.11 — google/skills: an official library.** Google's Cloud-product Skills
repository, installed like a package (`npx skills add google/skills`) across
thirty-plus agent hosts, exemplifies the same shift 3.4 named: vendors
publishing pre-built, versioned expertise as a first-class distribution
channel, in place of documentation pasted into context by hand.

**3.12 — last30days-skill: closing the knowledge-cutoff gap.** A
community-built skill that searches Reddit, X, YouTube, Hacker News,
Polymarket, GitHub, TikTok, Instagram, and Bluesky in parallel and ranks
results by actual community engagement — closing a real gap, since no single
mainstream AI platform searches across all of those surfaces at once.

**3.13 — Codebase Memory MCP: a map instead of a search.** Chapter 3 closes
on the same cost problem it opened with: grep-and-read burns roughly a
hundred input tokens per output token. A `tree-sitter`-based knowledge graph
of a repository's functions, classes, and call chains answers structural
queries at roughly ten times fewer tokens than file-by-file reading — and, in
the lesson's sharpest example, found all thirteen real call sites of a shared
lock that grep alone found zero of. A `PreToolUse` hook injects graph context
into the agent's existing grep calls automatically, sidestepping the failure
mode named back in 3.4: most specialised tools go unused because the agent
defaults to what it already has.

## Code

Chapter 2 restates the Chapter 1 loop almost unchanged; Chapter 3 mostly adds
infrastructure *around* that loop rather than changing it. The one new
structural piece worth keeping as a pattern is the six-step MCP loop from 3.2,
which every MCP-touching lesson in this guide (3.1, 3.3, 3.5, 3.8, 3.13)
assumes:

```python
def mcp_client_loop(servers: list, goal: str, max_steps: int = 10) -> str:
    catalog = {}
    for server in servers:
        for tool in server.list_tools():          # tools/list
            catalog[tool.name] = server

    messages = [{"role": "user", "content": goal}]
    for _ in range(max_steps):
        response = call_model(messages, tools=list(catalog.values()))
        if response.stop_reason == "end_turn":
            return response.text
        for call in response.tool_calls:
            server = catalog[call.name]
            result = server.call_tool(call.name, call.arguments)  # tools/call
            messages.append(tool_result_message(call, result))
    return "Max steps reached without completion."
```

Every MCP-specific lesson in Chapter 3 is a variation on where the servers in
`servers` come from (a hand-written weather server in 3.1, a security-audited
third-party one in 3.3, a browser page in 3.5, `agentmemory` in 3.8, a code
graph in 3.13) and what discipline surrounds this loop (context management in
3.6, retrieval in 3.7), not a change to the loop's shape.

## Verification

A reader has synthesised Chapters 2 and 3, not merely skimmed them, when they
can state four things without looking them up:

- **Why 2.1 and 2.2 insist on plain Python before a framework** — and the
  specific cost (3 to 8x) that makes "just add multi-agent" the wrong default
  answer to a struggling single agent.
- **The trust model MCP actually has**, in one sentence: a tool description
  is a prompt the agent reads, a server is a spawned local process, and
  security is the operator's job until the protocol grows integrity
  verification of its own.
- **Which of the four context-management strategies (3.6) applies to a given
  symptom** — a bloated system prompt is a compression problem, a large
  reference corpus is a retrieval problem, a multi-agent system leaking
  context between workers is an isolation problem.
- **Why a Skill going unused is almost always a description problem** (3.4),
  and why a code-search MCP going unused is almost always a discoverability
  problem the tool itself should solve via a hook (3.13) rather than a
  problem to fix by writing better documentation for the agent to ignore.

## Common Pitfalls

- **Reaching for multi-agent as the "advanced" default.** The measured 3–8x
  cost only pays for itself against genuine role specialisation or real
  parallel speed-up. See 2.2.
- **Trusting an MCP server because it looks clean today.** Rug pulls and
  cross-server hijacking both exploit exactly that assumption. See 3.3.
- **Treating a bigger context window as a free fix.** Context rot is
  measurable; more tokens can make an agent worse, not just more expensive.
  See 3.6.
- **Skipping the "answer only from provided sources" instruction in RAG.** A
  model without it fills retrieval gaps with fluent, unlabelled invention.
  See 3.7.
- **Writing a Skill description for a human reader.** It is a trigger signal
  for the model, and a description that does not match how a user actually
  asks is the single most common reason a Skill never fires. See 3.4.
- **Exposing a document converter's raw `convert()` method to user input.**
  It accepts arbitrary remote URIs; use `convert_local()` or
  `convert_stream()` instead. See 3.10.
- **Building a specialised tool and assuming the agent will choose it.** The
  more reliable pattern is a hook that enriches the agent's default tool
  rather than a new tool competing for the agent's attention. See 3.13.

## Related

- [[what-is-an-ai-agent]]
- [[the-agent-loop]]
- [[tool-use]]
- [[memory]]
- [[supervisor-worker-multi-agent]]
- [[mcp]]
- [[claude-code]]
- [[prompt-engineering]]
- [[best-practices-index]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]
- [[40_Guides/ai-agents-course-chapter-1-fundamentals|AI Agents Course — Chapter 1: Fundamentals]]

## Sources

- [[10_Sources/Blog/how-to-build-ai-agent-from-scratch|How to Build an AI Agent from Scratch in Python (2.1)]]
- [[10_Sources/Blog/multi-agent-system-python-tutorial|Multi-Agent System Python Tutorial (2.2)]]
- [[10_Sources/Blog/hermes-self-hosted-agent|Hermes Agent: Self-Hosted AI That Never Forgets You (2.3)]]
- [[10_Sources/Blog/gemma4-local-agents|Gemma 4: Free Agentic AI on Your Laptop (2.4)]]
- [[10_Sources/Blog/mcp-101-build-your-first-server|MCP 101: Build Your First MCP Server (3.1)]]
- [[10_Sources/Blog/mcp-internals-client-server|MCP Internals: STDIO, SSE, and JSON-RPC Explained (3.2)]]
- [[10_Sources/Blog/mcp-security-attack-vectors|MCP Security: 6 Attack Vectors and a 5-Step Audit (3.3)]]
- [[10_Sources/Blog/agent-skills-best-practices|Anthropic's 300+ Claude Code Skills: Lessons Learned (3.4)]]
- [[10_Sources/Blog/webmcp-complete-guide|WebMCP Tutorial: How Agents Use Websites as Tools (3.5)]]
- [[10_Sources/Blog/context-engineering-guide|Context Engineering: The Complete Guide (3.6)]]
- [[10_Sources/Blog/rag-vs-long-context-vs-fine-tuning|RAG vs Long Context vs Fine-Tuning (3.7)]]
- [[10_Sources/Blog/agentmemory-fix-memory-loss|Fix AI Agent Memory Loss in 30 Seconds (3.8)]]
- [[10_Sources/Blog/prompt-engineering-techniques-2026|Prompt Engineering in 2026: Techniques That Work (3.9)]]
- [[10_Sources/Blog/markitdown-pdf-to-markdown|MarkItDown: PDF to Markdown for RAG Pipelines (3.10)]]
- [[10_Sources/Blog/google-skills-official-library|google/skills: Google's Official Agent Skills Library (3.11)]]
- [[10_Sources/Blog/last30days-real-time-research-skill|last30days-skill: Real-Time Research for AI Agents (3.12)]]
- [[10_Sources/Blog/codebase-memory-mcp-guide|Codebase Memory MCP: Give Your Coding Agent a Map (3.13)]]

## See also

- [[MOC - Foundations]]
- [[MOC - Multi-Agent Systems]]
- [[MOC - MCP]]
- [[MOC - Tool Use]]
- [[MOC - Memory]]
- [[MOC - Prompt Engineering]]
- [[MOC - Security]]
- [[MOC - Best Practices]]
