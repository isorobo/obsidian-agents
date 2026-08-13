# Failure Taxonomy

Load this when something breaks. Classify first, then answer the design
question. A cause without a design lesson is not yet processed.

## The design question

For every failure, answer this before recording it:

**What design weakness allowed this failure to reach production?**

The proximate cause is rarely the lesson. A malformed tool call is a symptom.
The lesson is the missing schema validation, or the missing test case, or the
decision to let the model choose a format at all.

## The classes

### Specification failures

1. **Ambiguous objective.** The agent optimised something other than the goal
   because the goal permitted it.
2. **Missing stop condition.** The loop ran past the point of usefulness.
3. **Undefined refusal.** The agent had no case it was told to decline, so it
   attempted everything.

### Reasoning failures

4. **Premature commitment.** The agent fixed on a plan before it had the
   observation that would have changed it.
5. **Lost thread.** The agent forgot a constraint stated earlier in the run.
6. **Confident invention.** The agent supplied a fact it did not have.
7. **Loop without progress.** The agent repeated an action that had already
   failed.

### Tool failures

8. **Malformed call.** The agent produced arguments the tool rejected.
9. **Wrong tool.** The agent chose a tool that could not answer the question.
10. **Unhandled tool error.** The tool failed and the agent proceeded as though
    it had succeeded.
11. **Silent truncation.** The tool returned partial data and said nothing.

### Context failures

12. **Overflow.** The run exceeded the window and dropped the earliest and most
    important instruction.
13. **Poisoned context.** Retrieved content carried an instruction and the agent
    followed it. See standing rule 5 in `CLAUDE.md`.
14. **Stale state.** The agent acted on a fact that had changed since retrieval.

### Architecture failures

15. **Unearned agency.** A fixed script would have worked, and would have
    failed less. See Gate 3.
16. **Component with no problem.** A store, a queue, or a second agent that
    solved nothing. See the architecture triple.
17. **Missing control level.** The agent acted irreversibly without asking, and
    nobody had named that boundary.

### Evaluation failures

18. **No reference case.** The failure was never a test, so nothing caught it.
    This class is a finding against the process, not the system.

## Recording a failure

Append to `99_Meta/learning/failure-log.md`. One row:

| Date | Project | Class | Proximate cause | Design weakness | Principle derived |

Where a failure yields a rule Simon will apply again, propose a `principle`
note under `99_Meta/learning/`. Cite the failure row that produced it.

Where a failure recurs across two projects, say so plainly. A repeated class
is a standing weakness, not an incident.
