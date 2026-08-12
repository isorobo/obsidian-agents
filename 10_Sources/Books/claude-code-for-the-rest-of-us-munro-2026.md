---
type: source
status: draft
created: 2026-08-13
title: "Claude Code for the Rest of Us: A Non-Developer's Guide to AI-Powered Building"
authors:
- Harry Munro
organisation: Self-published
source_type: book
venue: 
url: TBD
year: 2026
date_published: 
anthropic: false
topic:
- topic/claude-code
- topic/best-practices
tags: [non-developers, claude-code, agent-skills, agent-teams, spec-driven-development, plugins]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
---

# Claude Code for the Rest of Us: A Non-Developer's Guide to AI-Powered Building

> Munro, H. "Claude Code for the Rest of Us: A Non-Developer's Guide to AI-Powered Building." Self-published, 2026. Copyright page: Copyright 2026 Harry Munro, first published 2026. No publisher is named. Extract held at `70_Research/_extracted/claude-code-for-the-rest-of-us.md`.

## Summary

Harry Munro writes for the reader who cannot code. The stated audience is product managers, designers, data analysts, operations leads, and project managers who work beside developers. The book runs to 24 chapters across six parts: foundations, core workflows, skills mastery, prototyping, the ecosystem, and reference. Its thesis holds that Claude Code accepts plain-language instruction, so the gap between a described idea and a working artefact closes. The book declines the promise of turning a reader into a developer. It offers self-sufficiency for prototypes, internal tools, and workflow automation.

The contrast with Anthropic's own [[10_Sources/Docs/claude-code-overview|Claude Code overview]] runs through the whole book. The official page states capability: surfaces, `CLAUDE.md`, skills, hooks, subagents, MCP, and the Agent SDK. It addresses a reader who ships software and who reads a diff to judge it. Munro addresses a reader who cannot read that diff. He spends a chapter on the terminal's reputation and the fear of breaking a machine. He rebuilds the safety case around permission prompts, plan mode, git commits, and scope limits, because code review is unavailable to his reader. The official docs teach features; this book teaches habits and a threshold for calling a professional.

## Key Concepts

- Six parts build on each other, and each chapter stands alone. Chapters carry a Concept or a Hands-on marker.
- Part I compares four tools in early 2026: Claude Code, Codex CLI, Gemini CLI, and OpenCode. Munro states his bias for Claude Code and ranks interactivity, explainability, and guardrails above learning curve and cost, because the reader cannot verify output by reading it.
- Part II covers the terminal, git, reading unfamiliar code, changing it under review, and testing. The reader approves commands rather than writing them.
- Part III covers skills: what a `SKILL.md` holds, how to install and invoke one, how to author one, five design patterns, and agent teams.
- Part IV covers web prototypes, internal tools, and deployment to a shared URL.
- Part V covers plugins, MCP servers, five named community projects, contributing back, and integrations with Linear, Notion, Slack, GitHub, and Firecrawl.
- Part VI holds a command reference, a context-management chapter, troubleshooting, and a glossary.
- The permission architecture is the book's centre of gravity. Read-only actions run without approval. Bash commands and file edits wait for the reader.

## Terminology

- **Terminal**. A text interface over the same operations a file browser performs. Munro treats fear of it as the first obstacle.
- **Plan mode**. A read-only research phase entered with `Shift + Tab` twice. Claude reads and proposes; nothing changes until the reader approves.
- **Rewind**. A restore point over conversation and file state, reached with `Escape` twice or `/rewind`.
- **Sandboxing**. Operating-system isolation of filesystem and network, added in October 2025. Anthropic's internal data puts the reduction in permission prompts at 84%.
- **Skill**. A file that captures a repeatable workflow. The `SKILL.md` format is an open standard, and both the reader and the model read the same file. Munro calls this dual legibility.
- **Agent teams**. Independent Claude Code instances that message each other and share a task list, distinct from subagents that report to one caller.
- **Nelson**. Munro's own skill that adds mission structure to agent teams: sailing orders, an estimate, a battle plan with file ownership, checkpoints, and a log.
- **Spec-driven development**. Producing an artefact that states the goal outside the conversation, then anchoring the work to it.
- **Context**. The working memory of a session: system instructions, history, files read, tool output, and reserved response space.

## Architecture and Implementation

The permission system has three tiers. Read-only file access needs no approval. A bash command needs approval before execution, and a standing approval binds to a project directory and a command. A file edit shows a diff first, and a standing approval lasts until the session ends. Sandboxing sits underneath: Seatbelt on macOS, bubblewrap on Linux and on Windows under WSL2, with network access confined to approved domains.

Agent teams have four components. A team lead spawns and directs. Teammates hold their own context windows and tools. A shared task list under `~/.claude/tasks/{team-name}/` tracks state and dependencies. A mailbox carries direct messages and broadcasts. The feature is experimental and gated behind an environment variable. Teammates run in one terminal by default, or in split panes under tmux or iTerm2. Three hook events fire on teammate idle, task creation, and task completion. Munro reports the coordination limit as file ownership: two teammates edit one file, each change is correct, and the merge fails.

The spec chapter sets out four artefact options. Markdown is the default and carries goal, out of scope, behaviour, and a done-means list. HTML suits visual work and stakeholder review. Markdown paired with structured JSON supports orchestration, which is the split Nelson uses. A database-backed store, as in the Beads project on Dolt, supports dependency queries at scale and survives a context reset.

## Code Examples

The book carries prompts and commands, not source listings. It teaches the reader to phrase a request, then approve the command Claude proposes. The reference chapter collects slash commands, keyboard shortcuts, CLI flags, environment variables, and a custom-agent JSON format. Named commands include `/plugin` for the marketplace, `/sandbox` for isolation settings, `/rewind` for restore points, `/context` for a token breakdown, and `/cost`, `/stats`, and `/status` for session state. Remote MCP servers install with one command, for example `claude mcp add -t http https://mcp.linear.app/mcp`. The markdown spec skeleton in Chapter 14 sits at about 100 words and remains the most reusable artefact in the book.

## Best Practices

- Commit to git before any ambitious change. A commit is the recovery point that rewind cannot replace.
- Enter plan mode for large or unfamiliar work. Separate research from execution.
- Review a proposed diff against four tests: scope, intent match, side effects, and reversibility.
- Convert a prompt into a skill once you have used it three times.
- Keep an agent team to three to five teammates, and assign file ownership before work starts.
- Write the spec outside the conversation. The spec is the artefact under your control when the code volume defeats line-by-line review.
- Run `/context` at the start of a session and after installing tools, since MCP servers and skills consume context without being used.
- Start with the official Anthropic marketplace and treat the verified badge as a signal. Install the fewest add-ons that solve a present problem.
- Keep internal tools single-user with read-only data connections. Hand off at the point login screens or production writes appear.
- Send anything touching sensitive data, financial transactions, or safety-critical decisions to a professional developer for review.

## Warnings and Anti-Patterns

The disclaimers open the book, and they carry the strongest warning in it. AI-generated code holds bugs, security holes, and logic errors, and it fails in different ways from human code. The reader owns the result: the model wrote it, the reader shipped it.

- Rewind tracks direct file edits alone. A file changed inside a bash command falls outside it. Git remains the reliable net.
- Scope creep recurs. A request to change one colour returns edits across five files. Munro treats this as routine behaviour, not an aberration.
- Agent teams fail on file collisions, conflicting changes, and token cost. Munro reports a refactor that produced three correct and incompatible pieces of work.
- A forgotten tunnel leaves a local machine reachable from the internet for days.
- A polished prototype creates production expectations the reader cannot meet. A rough one sets a truer expectation.
- Plugin rot, configuration conflicts between plugins, and a false sense of security from star counts and badges all bite. Verification stays with the reader.
- Context degrades before it runs out. The model drops earlier instruction without announcing it.
- Internal tools drift towards products. The spreadsheet replacement trap leaves a team maintaining both systems, because the mess in the old sheet encoded edge cases.
- The book states that Claude assisted its drafting, and that early-2026 model names, limits, and interfaces expire.

## Related Concepts

- [[claude-code]]
- [[mcp]]
- [[prompt-engineering]]
- [[plan-and-execute]]
- [[supervisor-worker-multi-agent]]
- [[workflow-vs-autonomous-agent]]
- [[best-practices-index]]
- [[anti-patterns-index]]
- [[10_Sources/Docs/claude-code-overview|Claude Code overview]]
- [[10_Sources/Interviews/boris-cherny-pragmatic-engineer|Boris Cherny on Claude Code]]
- [[10_Sources/Blog/anthropic-building-effective-agents|Building effective agents]]

## Future Work

Munro flags agent teams as experimental, with an interface that shifts between versions. He names remote MCP servers as the 2026 shift, since OAuth-secured hosted servers remove local processes and stored keys. The integrations chapter closes on a pattern he leaves open: agents of different people coordinating through shared tools such as Linear and Slack rather than through direct agent-to-agent channels. The disclaimer states that principles hold while specifics expire, and directs the reader to the documentation when a described option has moved.

## References

- Extract: `70_Research/_extracted/claude-code-for-the-rest-of-us.md`
- Anthropic. Claude Code plugins documentation. https://code.claude.com/docs/en/plugins
- Anthropic. Claude Plugins Official repository. https://github.com/anthropics/claude-plugins-official
- Agent Skills. `SKILL.md` specification. https://agentskills.io
- Model Context Protocol. Official servers repository. https://github.com/modelcontextprotocol/servers

## See also

- [[agent-patterns-index]]
