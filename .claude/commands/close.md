---
description: Review the session, then propose notes, ledger rows, and gaps for approval.
argument-hint: [optional project slug to run the full audit]
---

Close the session. Load `Skill(learn-agents)` and its `references/capture.md`.

Where `$ARGUMENTS` names a project, also load `references/project-audit.md`
and run all 50 questions before proposing anything.

Output in this order:

## 1. Session review

Four lines, no padding:

- What Simon set out to do.
- What was built or decided.
- What it taught, stated as a concept, not as an activity.
- What remains unresolved.

Where the session taught nothing, say so. Do not manufacture a lesson.

## 2. Proposed notes

Number each one. For each, give the target path, the full frontmatter, and a
preview of the body. Follow the destination table in `references/capture.md`
and the templates in `90_Templates/`.

Flag any note that would need a new controlled `type` or `topic` value. That
schema update is its own numbered item and lands first.

## 3. Proposed ledger rows

A table of the rows that would change in `99_Meta/learning/ledger.md`, each
with its evidence. Advance nothing on reading alone.

## 4. Proposed failure rows

A table of rows for `99_Meta/learning/failure-log.md`. Each row names the class
from `references/failure-taxonomy.md` and the design weakness that allowed the
failure. A row with a cause but no design lesson is not ready. Say so.

## 5. Proposed gaps

Each question the vault could not answer, as a `00_Inbox/gap-<slug>.md` item.

## 6. Approval

Ask Simon which numbers to write. Write nothing before he answers. This
approval is the only human gate left, because the vault runs under
`permissionMode: yolo` and `safeMode: acceptEdits`.

After writing, confirm each path and stop.
