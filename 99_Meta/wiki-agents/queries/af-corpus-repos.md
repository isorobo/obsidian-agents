# Query plan - af-corpus-repos

Base surface: see `watchlist.md` channel surface notes. Feeds agent-factory RSCH-01 (one-way digest).

## Window
- since_date: 2023-01-01 (repository content is studied regardless of age; dedupe governs)

## Fetch method
- WebFetch `https://api.github.com/repos/<owner>/<repo>` (metadata, default branch), `.../contents/<path>` for docs, `.../releases?per_page=10`; file bodies via `https://raw.githubusercontent.com/<owner>/<repo>/HEAD/<path>`.
- Fallback: WebFetch `https://raw.githubusercontent.com/<owner>/<repo>/<default branch>/<path>`.
- Repositories (no others): `humanlayer/12-factor-agents`, `hardness1020/learn-agent-architecture`, `SWE-agent/mini-swe-agent`, `huggingface/smolagents`.

## Include filters
- one overview note per repository (README: purpose, structure, core loop, key claims)
- 12-factor-agents: the factor documents (prompts, context window, tools as structured output, execution and business state, launch, pause and resume, human contact, control flow, error compaction, small focused agents, triggers, stateless reducer)
- learn-agent-architecture: the chapters on agent loop, tools, permissions, context, memory, tasks, interfaces, planning, subagents, skills, sessions, recovery, evaluation, and its comparisons of real implementations (Claude Code, mini-SWE-agent, Hermes, DeepSeek harness)
- mini-swe-agent: the core agent and environment code paths and the docs that explain why it is minimal (bash-only actions, linear history, stateless subprocess execution)
- smolagents: docs and source on the step loop, CodeAgent versus ToolCallingAgent, model invocation, tool execution, memory and message handling, termination, managed agents, sandboxed execution
- releases that change the architecture of any of the four

## Exclude filters
- other repositories, forks, mirrors and blog rewrites of these repositories
- per-model integration pages, installation-only pages, contributor guides
- patch releases with no architectural change
- duplicates of existing source notes

## Priority
1. Overview notes: 12-factor-agents, learn-agent-architecture, mini-swe-agent, smolagents
2. Parts that answer agent-factory research questions not yet covered (see the latest digest's RSCH-04 coverage)
3. Remaining parts, then architectural releases
