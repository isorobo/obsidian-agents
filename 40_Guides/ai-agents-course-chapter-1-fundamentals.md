---
type: guide
status: draft
created: 2026-07-11
name: "AI Agents Course — Chapter 1: Fundamentals (Synthesis)"
slug: ai-agents-course-chapter-1-fundamentals
topic:
- topic/foundations
tags: [ai-builder-club, course-notes, tool-use, memory, multi-agent, deployment, karpathy]
synonyms: ["AI Builder Club Chapter 1", "Build AI Agents Course — Fundamentals"]
related_concepts:
- "[[what-is-an-ai-agent]]"
- "[[agent-vs-llm]]"
- "[[the-agent-loop]]"
- "[[tool-use]]"
- "[[memory]]"
- "[[supervisor-worker-multi-agent]]"
- "[[claude-code]]"
- "[[mcp]]"
---

# AI Agents Course — Chapter 1: Fundamentals (Synthesis)

> A single, synthesised map of AI Builder Club's "Build AI Agents Course" Chapter 1 (lessons 1.1 through 1.12), from the first agent loop to Karpathy's framing of the field.

## Goal

This guide compresses twelve lessons of AI Builder Club's Chapter 1: Fundamentals
into one reading. A reader finishes with the same working model of an AI agent
that the full chapter builds lesson by lesson — what an agent is, how it calls
tools, how it remembers, how it coordinates with other agents, how it deploys,
and how Andrej Karpathy's 2026 public statements reframe the discipline around
all four. The guide replaces eleven separate blog posts, not the two videos
(1.1 and part of 1.3 and 1.6), which remain video-only and are not filed as
sources here.

## Prerequisites

- Comfort reading Python and one LLM SDK (Anthropic or OpenAI); every code
  pattern below assumes both.
- Familiarity with [[what-is-an-ai-agent]] and [[agent-vs-llm]] helps but is
  not required — Part One rebuilds both from scratch.

## Steps

Read the four parts in order. Parts One and Two build the mechanics; Parts
Three and Four build the judgment to use them.

### Part One: The Agent Loop and Tool Use (1.2 – 1.4)

**1.2 — What is an agent.** An agent is a software loop that uses a language
model to decide what to do next, does it, checks the result, and decides
again until the goal is reached. A chatbot answers once and stops; an agent
repeats the cycle on an identical underlying model — the wrapper, not the
model, makes the difference. Every agent needs four components: the brain
(the LLM, which decides but never executes), tools (the actions it can take),
memory (continuity across stateless calls), and the loop (the orchestrator
code that ties the three together). A roughly 40-line reference
implementation — register tools in a dictionary, send messages and schemas to
the model each turn, execute what it requests, feed the result back, repeat
until `end_turn` or `max_steps` — is the complete pattern underneath every
framework built since.

**1.3 — Function calling.** Before native tool-calling, builders regex-parsed
freeform model output and ran a 15–25% JSON failure rate. Function calling
replaced this with a three-step cycle — **menu** (the request declares
available tools and schemas), **order** (the model returns structured JSON
naming a tool and its arguments), **serve** (application code executes it and
returns the result). The model never touches a system directly; it only ever
decides what to request. Reliability comes from constrained decoding at
inference time, which makes an out-of-schema token mathematically
unreachable, not merely unlikely. Tool descriptions function as prompt
engineering: write them as *when to use this*, not *what this does*, cap
parameters at five to eight, lock enumerable values with `enum`, and keep
schemas to three nesting levels or argument accuracy degrades.

**1.4 — Giving the agent real tools.** The Part 1 agent could only read local
files and crashed on any tool failure. Part 1.4 adds web search, code
execution, and file writing, and treats error handling as a first-class
design problem, not an afterthought. Every external call returns a structured
error with a `retry` flag rather than an opaque string, so the model — not
hard-coded logic — decides whether to reattempt. Code execution writes
untrusted code to a temp file and runs it as a subprocess with a timeout,
never `eval()` or `exec()` directly, and requires real sandboxing (E2B,
Modal, Docker) before production. File writes need `pathlib.Path.
is_relative_to()` for path-traversal defence — a naive `startswith()` check
lets a sibling directory like `/project-evil` pass validation against a root
of `/project`. Tool count has a measured accuracy ceiling: about ten tools
hold 95%+ selection accuracy, thirty drop to roughly 85%, and beyond fifty
needs deferred loading or splitting.

### Part Two: Memory (1.5 – 1.6)

**1.5 — Memory across sessions.** Every LLM API call is stateless — the model
carries no memory of its own between calls — so persistence is entirely the
developer's problem to solve. Three patterns cover increasing durability:
**in-context** memory (the current message list, gone when the session ends),
**external file** memory (Markdown or JSON on disk, human-readable, breaks
down past roughly fifty thousand tokens of accumulated fact), and **vector
database** memory (semantic retrieval, scales to thousands of facts). The
progression is deliberate: start in-context, move to a file once persistence
matters, add a vector store only once the file becomes unwieldy — not before.

**1.6 — The full memory taxonomy.** This lesson reframes memory through a
cognitive-science lens: **episodic** memory (what happened — past
conversations, which approach failed), **semantic** memory (factual truths —
preferences, stack details), and **procedural** memory (learned methods — a
debugging routine). A mature agent needs all three; semantic-only memory
misses experiential learning, episodic-only over-weights anecdotes. The
central claim is that **quality is set at the write stage, not the retrieval
stage** — a memory system that writes carelessly cannot be rescued by clever
search. The full lifecycle is write, maintain, retrieve, and the maintain
phase — merging duplicate facts, updating superseded ones, forgetting by age
and importance rather than raw access frequency — is the phase most systems
skip. Three production architectures compare on transparency versus
infrastructure cost: MemGPT/Letta pages between a context window and an
external store across core/recall/archival tiers; Mem0 automates
extraction and reconciliation and beat full-context stuffing on the LOCOMO
benchmark; Claude Code stores memory as plain, git-versionable Markdown with
zero infrastructure and total transparency, at the cost of no semantic
search. The synthesis line worth keeping: *context is RAM, visible now, gone
at session end; memory is disk, persistent but useless until retrieved; the
bridge between them — retrieval — is where memory systems are actually won.*

### Part Three: Multi-Agent Systems and Production (1.7 – 1.8)

**1.7 — Multi-agent orchestration.** A single agent hits scaling limits on
complex tasks: its context window fills, it loses earlier findings, and it
works sequentially. Three patterns address this. **Pipeline** — Agent A to B
to C, each stage seeing only its predecessor's output, best for fixed
transformation sequences, but errors compound past four or five steps.
**Supervisor/worker** — a coordinator decomposes a task and routes subtasks
to isolated specialists, then synthesises; the supervisor plans and
synthesises but never executes domain work itself. **Fan-out** — one task
split into N parallel executions via `asyncio.gather(..., return_exceptions=
True)`, turning 25–50 seconds of sequential work into 5–10 seconds, at the
cost of multiplied rate-limit exposure. Five rules keep any of the three
predictable: single responsibility per agent; no direct agent-to-agent
communication, only orchestrator-mediated handoffs; aggressive context
trimming between stages; assume partial failure with multiple workers; and
the supervisor executes nothing.

**1.8 — Production deployment.** Agents break three standard web-service
assumptions: bounded latency (a run can take 30 seconds to indefinitely),
deterministic cost (a bug can trigger thousands of silent calls), and legible
failure (an agent can look complete while producing garbage, with no HTTP
500 to flag it). A VPS suits agents running past 60 seconds or on a schedule;
serverless suits short webhook-triggered tasks. Every dependency version gets
pinned — a minor SDK bump has broken production agents before — and the
container runs as a non-root user with `--restart unless-stopped`. Real
health checks verify dependencies (model API reachability, memory-store
connectivity, disk space), not just process liveness, and split into a fast
`/ping` liveness probe and a real `/health` readiness probe. Structured JSON
logging (`structlog`) records every loop step — call start, response with
token counts, tool call start/complete/fail — bound to a `run_id` so a cost
spike is traceable. Cost control needs three independent layers: a per-run
token budget that raises an exception when exceeded, a thread-safe daily
spend tracker written to disk against a hard dollar limit, and a
provider-dashboard hard limit at roughly twice expected spend as the final
backstop. Deployments that blow past budget are, per the lesson, always
missing the first layer specifically.

### Part Four: Karpathy's Frame (1.9 – 1.12)

These four lessons are AI Builder Club's commentary on Andrej Karpathy's 2026
public talks and posts — explicitly not his own words — and reframe Parts One
through Three as professional practice rather than mechanics. See
[[20_People/andrej-karpathy/profile|Andrej Karpathy]] for the person and
[[20_People/ai-builder-club/profile|AI Builder Club]] for the publisher.

**1.9 — Agentic engineering versus vibe coding.** Vibe coding is rapid,
low-oversight AI-assisted development with no quality bar — code that runs
but a product that still breaks, illustrated by a case of cross-matching
different email systems that silently corrupted user credits. Agentic
engineering is the professional alternative: five skills — spec design, diff
review, eval design, security oversight, and quality taste — practised
deliberately. A December 2025 reliability inflection point, where larger
generated chunks began consistently landing correct, shifted programming from
writing lines to delegating macro actions, which made this discipline daily
practice rather than occasional experiment. As generation gets absorbed,
understanding, taste, system-design judgment, eval design, and agent
orchestration become the scarcer, more valuable human skills.

**1.10 — agents.md and permission boundaries.** A formal `AGENTS.md` standard
already exists under Linux Foundation stewardship, read by most major coding
tools; Claude reads `CLAUDE.md`, Gemini reads `GEMINI.md`. This lesson
synthesises four themes from Karpathy's public statements into four proposed
rules for an agent-specific version: define permission boundaries explicitly
(READ / WRITE / NEVER / HUMAN_CHECKPOINT) before writing code; make every
tool action reversible or fully auditable, gating irreversible ones behind
human approval; fail loudly and stop on an out-of-scope situation rather than
improvise past it; and treat a persistent Markdown memory file, not the
model's context window, as the source of truth. The underlying claim: agent
failures concentrate at tool handoffs and ambiguous instructions, not core
capability gaps, so oversight should scale with an action's *reversibility*,
not its complexity.

**1.11 — Software 3.0.** Karpathy names three eras: Software 1.0 is explicit
code, 2.0 is trained network weights, 3.0 is the context window itself as the
program, with the LLM as interpreter. This is framed as categorical, not
incremental — the MenuGen example collapses a multi-service stack (upload,
OCR, image generation, UI) into one multimodal prompt, and "the entire app
architecture disappears." The practical filter this lesson keeps: AI
capability improves fastest wherever a domain has an automatic, verifiable
success signal (tests pass, code compiles) — traditional software automates
what you can *specify*; LLMs automate what you can *verify*. Build
agent-native infrastructure — Markdown docs, CLIs, MCP servers, structured
logs — as a first-class target, not an afterthought to a human-facing UI.

**1.12 — The LLM wiki pattern.** Standard RAG retrieves chunks per query and
accumulates nothing across sessions. Karpathy's alternative has the model
maintain a persistent, compounding Markdown wiki across three layers — raw
sources (immutable, read-only), the wiki (entirely LLM-owned), and a schema
file (`CLAUDE.md`/`AGENTS.md` defining structure and workflow) — driven by
three operations: **ingest** (read a source, write a summary, touch ten to
fifteen relevant pages), **query** (search, synthesise, cite, file good
answers back as new pages), and **lint** (a periodic pass catching
contradictions, stale claims, and orphan pages). Karpathy's own framing:
"Obsidian is the IDE. The LLM is the programmer. The wiki is the codebase."
The bottleneck human-maintained wikis hit is bookkeeping, not thinking — and
that is exactly the part an LLM does not get bored of. **This vault,
`wiki-agents`, is a working instance of the pattern this lesson describes.**

## Code

The single pattern underneath every lesson in this chapter is the loop from
1.2, extended by the error handling from 1.4:

```python
def run_agent(goal: str, max_steps: int = 10) -> str:
    messages = [{"role": "user", "content": goal}]
    for _ in range(max_steps):
        response = call_model(messages, tools=TOOL_SCHEMAS)
        if response.stop_reason == "end_turn":
            return response.text
        for call in response.tool_calls:
            try:
                result = TOOLS[call.name](**call.arguments)
            except Exception as exc:
                result = {"error": str(exc), "retry": False}
            messages.append(tool_result_message(call, result))
    return "Max steps reached without completion."
```

Every later lesson in this chapter — tools, memory, multi-agent, production —
extends this loop rather than replacing it: tools populate `TOOLS`, memory
populates `messages` at start and end, multi-agent runs several of these
loops under an orchestrator, and production wraps it in logging, health
checks, and a token budget.

## Verification

A reader has synthesised this chapter, not merely skimmed it, when they can
state four things without looking them up:

- **The four-component model** — brain, tools, memory, loop — and where each
  of the later lessons (1.3–1.8) slots into it.
- **The trigger for the next tier of complexity** in both tool design (why
  add a tenth tool, why sandbox code execution) and memory design (why move
  from in-context to file, from file to vector store).
- **The distinction Karpathy draws** between vibe coding and agentic
  engineering, and why oversight should scale with reversibility rather than
  task complexity.
- **Why Software 3.0 and the LLM wiki are the same claim from two angles** —
  a domain with a verifiable success signal lets an LLM own work no classical
  program could reliably do, whether that work is code or knowledge
  maintenance.

## Common Pitfalls

- **Skipping the result-feedback step.** An agent that never sees its own
  tool results is blind to its actions and repeats them. See 1.2.
- **String-parsing model output instead of native tool-calling.** Reintroduces
  the 15–25% failure rate function calling was built to eliminate. See 1.3.
- **Reaching for a vector database before a file has actually failed.**
  Premature complexity in memory design mirrors premature complexity in
  multi-agent design — earn each tier with an observed failure. See 1.5, 1.6.
- **Direct agent-to-agent communication.** Bypassing the orchestrator in a
  multi-agent system produces unpredictable shared state. See 1.7.
- **Deploying without a per-run token budget.** The single most common cause
  of runaway agent cost, per 1.8.
- **Treating agentic-engineering discipline as optional at speed.** Skipping
  spec design and diff review because an agent "just works" is vibe coding
  by another name. See 1.9.
- **Scaling oversight to task complexity instead of action reversibility.**
  Misallocates review effort — a complex but fully reversible action needs
  less gating than a simple but irreversible one. See 1.10.

## Related

- [[what-is-an-ai-agent]]
- [[agent-vs-llm]]
- [[the-agent-loop]]
- [[tool-use]]
- [[memory]]
- [[supervisor-worker-multi-agent]]
- [[workflow-vs-autonomous-agent]]
- [[claude-code]]
- [[mcp]]
- [[evaluation]]
- [[best-practices-index]]
- [[20_People/andrej-karpathy/profile|Andrej Karpathy]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Sources

- [[10_Sources/Blog/ai-agents-101-what-is-an-agent|What Is an AI Agent? (1.2)]]
- [[10_Sources/Blog/function-calling-how-llms-use-tools|Function Calling Explained (1.3)]]
- [[10_Sources/Blog/ai-agents-101-tools-in-python|AI Agent Tools in Python (1.4)]]
- [[10_Sources/Blog/ai-agents-101-memory-across-sessions|AI Agent Memory Across Sessions (1.5)]]
- [[10_Sources/Blog/agent-memory-systems-guide|Agent Memory Systems: The Complete Guide (1.6)]]
- [[10_Sources/Blog/ai-agents-101-multi-agent-orchestration|Multi-Agent Orchestration Patterns (1.7)]]
- [[10_Sources/Blog/ai-agents-101-deploy-to-production|Deploy AI Agents to Production (1.8)]]
- [[10_Sources/Blog/karpathy-agentic-engineering-framework|Agentic Engineering: Karpathy's New Framework (1.9)]]
- [[10_Sources/Blog/karpathy-agents-md-framework|Karpathy's agents.md (1.10)]]
- [[10_Sources/Blog/karpathy-software-3-0|Karpathy's Software 3.0 (1.11)]]
- [[10_Sources/Blog/karpathy-llm-wiki-pattern|Karpathy's LLM Wiki (1.12)]]

Lesson 1.1, "AI Agents: The Complete 2026 Roadmap", is a video on the course
landing page with no companion article and is not filed as a source note.

## See also

- [[MOC - Foundations]]
- [[MOC - Tool Use]]
- [[MOC - Memory]]
- [[MOC - Multi-Agent Systems]]
- [[MOC - Deployment]]
- [[MOC - Best Practices]]
