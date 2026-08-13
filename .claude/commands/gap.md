---
description: File a question the vault could not answer into 00_Inbox for research.
argument-hint: [the question]
---

Record `$ARGUMENTS` as a vault gap.

A gap file is a research brief. It is not an answer. Never write the answer
from model knowledge into it. The research pipeline resolves it from primary
sources.

Steps:

1. Search the vault first. Where a note already answers the question, cite it
   and stop. A gap that is not a gap wastes a research run.
2. Where the vault answers it partially, say which part is covered and scope
   the gap to the remainder.
3. Propose `00_Inbox/gap-<slug>.md` with `type: draft`, `status: inbox`, the
   controlled topic values it belongs to, and a body holding:
   - The question, in one sentence.
   - Why it arose. Name the session or project.
   - What the vault holds nearby, with wikilinks.
   - What a good source would look like. Primary material only.
4. Where the gap justifies a new controlled `topic` value, say so and propose
   the `99_Meta/schema.md` update as a separate item. The schema changes first.

Write nothing until Simon approves.
