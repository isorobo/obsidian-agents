# wiki-agents — Agent Session Conventions

This vault documents AI Agents with the Anthropic ecosystem as the primary lens.
Read this before editing.

## Structure

- Functional folder spine. Topics live as MOCs and the controlled `topic`
  vocabulary, not as folders. See `99_Meta/schema.md`.
- One idea per note. Kebab-case slugs. MOCs named `MOC - <Name>`.

## Rules

- Every note carries `type`, `status`, `created`, `topic`, `tags`.
- A new controlled value requires a `99_Meta/schema.md` update first.
- Every note links to its topic MOC and at least one related note. No orphans.
- Sources cite primary material. Anthropic sources set `anthropic: true`.
- Templates live in `90_Templates/`. Use them for new notes.

## Pipeline

- The watchlist at `99_Meta/wiki-agents/watchlist.md` drives research runs.
- Per-channel state under `99_Meta/wiki-agents/state/`.
- Workflows documented in `99_Meta/wiki-agents/`.

## Do not

- Do not add topical top-level folders. Extend the `topic` vocabulary instead.
- Do not break Dataview queries in MOCs.
- Do not commit binaries; `10_Sources/PDFs/` is git-excluded.

## Design of record

`99_Meta/design/2026-07-10-wiki-agents-foundation-design.md`.
