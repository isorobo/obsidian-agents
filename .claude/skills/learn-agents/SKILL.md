---
name: learn-agents
description: The eight-gate design protocol for wiki-agents. Use when Simon starts a new agent project, makes an architecture decision, classifies a failure, closes a project, or captures what a session taught. Enforces learning objective before architecture, the agency test before design, simplest-sufficient bias, vault citation, and evaluation before a stage closes. Invoked by Design mode in CLAUDE.md and by /design, /close, and /learn.
---

# learn-agents

The Design protocol for the wiki-agents vault. `CLAUDE.md` holds the always-on
contract. This skill holds the depth, loaded only when Simon designs something.

Read `CLAUDE.md` first. Its five standing rules bind everything below.

## When to run

Run the eight gates for a new project, a change of architecture, or a decision
Simon will have to defend later. Do not run them for a question, a bug, or a
small change. Those are Ask mode and Build mode.

## The eight gates

Work the gates in order. State the gate number and its answer. Each gate cites
a vault note or declares a gap. Do not write code in this mode.

### Gate 1. Learning objective

Name the one concept this project exists to teach. Write it before anything
else. A project with no learning objective is a task, not a project. Say so
and drop to Build mode.

Check the objective against `99_Meta/learning/ledger.md`. If the objective sits
more than two rows ahead of Simon's furthest `applied` concept, name the gap
and propose the prerequisite instead.

### Gate 2. Problem definition

State the problem in one sentence, without naming a technology. State the
input, the output, and the test that says it worked. A problem that resists a
one-sentence statement is two problems. Split it.

### Gate 3. The agency test

Compare three solutions before designing an agent:

| Option | Fits when |
|---|---|
| Fixed code | The steps are known and stable. |
| Scripted LLM workflow | The steps are known; the language handling varies. |
| Agent | The steps are unknown until run time. |

Cite [[workflow-vs-autonomous-agent]]. Recommend the least agentic option that
solves the problem. Where the agent wins, name the specific run-time unknown
that forces it. No unknown, no agent.

### Gate 4. The agent's job

State what the agent decides. An agent that decides nothing is a script.
State what it may not decide, and who decides it instead.

### Gate 5. The loop

Describe one iteration: the trigger, the observation, the decision, the action,
and the stop condition. Cite [[the-agent-loop]]. An unbounded loop is a
defect. Name the maximum iterations and what happens at the limit.

### Gate 6. Planning

State whether the agent plans. Where it plans, choose the pattern and say why:
react for interleaved reasoning and action, plan-and-execute for a fixed
sequence known up front, reflexion for a retry that learns from the last
attempt. Cite [[react]], [[plan-and-execute]], or [[reflexion]]. Where the
agent does not plan, say so, and say what supplies the order instead.

### Gate 7. Tools and pattern

Call `Skill(agens)` for the pattern recommendation. Do not select a pattern
here. Agens owns pattern selection, cites
`30_Concepts/agent-patterns-index.md`, and logs to `99_Meta/agens-log.md`.
Two systems answering the same question is the defect this gate exists to
prevent.

List each tool the agent needs. For each: what it does, what it returns, and
what it costs if it is wrong. Cite [[tool-use]]. A tool with no failure mode
stated is a tool not yet understood.

### Gate 8. Knowledge and memory

State what the agent must know at start, what it must retain within a run, and
what it must retain across runs. Cite [[memory]]. Retrieval is the lookup
mechanism; memory is the retained state. Do not conflate them. Where nothing
must be retained across runs, say so and delete the store.

## After the gates

### Architecture triple

Give three architectures, always in this order:

1. **Minimum.** The least that satisfies Gate 2's test. Ship this first.
2. **Recommended.** The minimum plus the components Simon can justify today.
3. **Future.** What earns a place once the system runs and the data exists.

For every component in every tier, state the problem it solves. Delete any
component with no answer. Naming a technology is not an answer.

### Implementation stages

Break the recommended architecture into stages. Each stage runs end to end and
produces something observable. No stage closes without one check that failed
before the change and passes after it. State that check as a command or as an
observation Simon can make. A stage with no check does not close.

### Evaluation

Before the first stage starts, name three cases: one the system must handle,
one edge case, and one it must refuse. Write them down. They are the reference
set. Cite [[evaluation]].

### Control levels

State who holds the stop. Name the point at which the agent acts without
asking, and what it may never do without asking. Given this vault runs under
`permissionMode: yolo`, an unnamed control level means no control level.

## Failure handling

When something breaks, load `references/failure-taxonomy.md`. Classify the
failure, then answer the question that matters: what design weakness allowed
it. A failure with a cause but no design lesson is not yet processed. Record
it in `99_Meta/learning/failure-log.md`.

## Closing a project

Load `references/project-audit.md` and run it. Then load
`references/capture.md` to map what the project taught into vault notes.
Propose every note. Write nothing without approval.

## Style

Follow `~/.claude/rules/drafting-style.md`. NZ English. No em dashes. Short
sentences. State positions as fact. No praise, no preamble.
