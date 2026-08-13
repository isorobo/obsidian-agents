# Capture

How a session's output becomes vault notes. Load this at `/close` or when
Simon says a session produced something worth keeping.

## The rule

Nothing is written without approval. Propose each note with its target path,
its full frontmatter, and a preview of its body. Simon replies with the numbers
he approves. Given the vault runs under `permissionMode: yolo` and
`safeMode: acceptEdits`, this approval step is the only remaining human gate.

## What earns a note

| Output | Destination | Type |
|---|---|---|
| A concept the vault lacked | `30_Concepts/<slug>.md` | `concept` |
| A design pattern Simon used | `30_Concepts/<slug>.md` | `pattern` |
| A mistake worth naming | `30_Concepts/<slug>.md` | `anti-pattern` |
| A build and what it taught | `99_Meta/learning/projects/<slug>.md` | `project` |
| One failure and its design lesson | row in `99_Meta/learning/failure-log.md` | n/a |
| A rule derived from a failure | `99_Meta/learning/principles/<slug>.md` | `principle` |
| A question the vault could not answer | `00_Inbox/gap-<slug>.md` | `draft` |
| A step-by-step method | `40_Guides/<slug>.md` | `guide` |

A session that produced none of these produced no note. Say so. Do not
manufacture one.

## Frontmatter

Every note carries `type`, `status`, `created`, `topic`, `tags`. See
`99_Meta/schema.md` section 2.1. A value outside the controlled vocabulary
requires a schema update first, proposed as its own numbered item.

`project`, `failure`, `principle`, and `ledger` notes carry `topic/learning`
plus one general topic.

Set `authored_by: agens` only on notes the agens skill writes. A note written
under this skill is a proposal Simon approved, so it carries no such marker.

## Body structure

Use the templates in `90_Templates/`. Do not invent a structure.

A concept note follows `template - concept.md`: Summary, Key Concepts, Detail,
Trade-offs and Limits, Related, Sources, See also.

A `project` note follows the same skeleton, with these sections:

- **Objective.** The learning objective, stated before the build.
- **Problem.** One sentence. Input, output, test.
- **Architecture.** Which tier shipped, and which components were cut.
- **What it taught.** The concepts moved on the ledger, with evidence.
- **Failures.** Links to failure-log rows.
- **Related.** Three concept links, minimum.
- **See also.** `[[MOC - Meta]]`.

A `principle` note states the rule in one sentence, then cites the failure or
project that produced it. A principle with no source is an opinion. Do not
write it.

## Linking

The vault forbids orphans. Every proposed note links to its topic MOC, and the
MOC gains a link back. Every concept links to at least three related concepts.
Where three do not exist, say so rather than padding the list.

## Gap files

A gap file records a question the vault could not answer. It is a research
brief, not an answer. Body: the question, why it arose, what the vault does
hold nearby, and what a good source would look like. Never write the answer
from model knowledge into a gap file. The research pipeline resolves it from
primary sources.

## Citations

Cite primary material. A source with tracking parameters in its URL, or one
that cannot be reached, carries `[VERIFY]` beside it and does not seed a
source note until checked.
