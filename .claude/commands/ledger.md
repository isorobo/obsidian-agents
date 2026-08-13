---
description: Show learner state and propose evidence-based updates to the ledger.
argument-hint: [optional concept slug]
---

Read `99_Meta/learning/ledger.md`.

With no argument, report:

1. The furthest concept at `applied` or beyond. That is the ceiling standing
   rule 1 enforces.
2. Every concept at `explained` that has never been applied. Those are the
   ones at risk of being forgotten.
3. The next three concepts at `not-started`, in reading order.
4. Every open question recorded against a row.

With a concept slug, report that row alone, then ask what evidence supports a
change.

Rules for a change:

- Status advances on evidence, never on reading. Name the evidence in the row.
- `explained` requires Simon's own restatement, not Claude's explanation.
- `applied` requires something built.
- `debugged` requires a failure Simon fixed, linked to `failure-log.md`.
- `taught-back` requires Simon explaining it unaided.
- A status may move backwards. Say so plainly where the evidence has gone
  stale.

Propose the edited rows as a table. Write nothing until Simon approves.
