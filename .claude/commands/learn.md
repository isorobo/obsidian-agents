---
description: Teach one concept from the vault, then propose a ledger update.
argument-hint: [concept slug or question]
---

Teach the concept named in `$ARGUMENTS`. If no argument is given, read
`99_Meta/learning/ledger.md` and teach the first concept at `not-started`.

Follow `CLAUDE.md`. This is Ask mode with one addition: end by testing whether
Simon can restate it.

Steps:

1. Find the concept note in `30_Concepts/`. Cite its path. Where no note
   exists, say so, teach from model knowledge, and propose a gap file.
2. Check the ledger. Where Simon has not reached the concepts this one depends
   on, name the prerequisite and offer to teach that instead.
3. Teach in under 300 words. Definition, why it matters, one concrete example,
   and the failure it prevents.
4. Ask one question that only someone who understood it can answer. Do not
   answer it yourself.
5. Propose the ledger row. `explained` lands only after Simon restates it in
   his own words. Reading advances nothing.

End with the ledger stamp.
