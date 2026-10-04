# Query plan - arxiv-agents

Base surface: see `watchlist.md` channel surface notes.

## Window
- since_date: 2026-07-10 (vault foundation; arXiv volume is high, so newest first)

## Fetch method
- arXiv API via WebFetch: `http://export.arxiv.org/api/query?search_query=(cat:cs.AI+OR+cat:cs.MA)+AND+(abs:agent+OR+abs:%22tool+use%22+OR+abs:planning+OR+abs:%22multi-agent%22+OR+abs:reflexion+OR+abs:ReAct)&sortBy=submittedDate&sortOrder=descending&max_results=50`
- Read the abstract page `https://arxiv.org/abs/<id>` before accepting.

## Include filters
- LLM agent architectures: the agent loop, harnesses, runtimes, agent-computer interfaces
- tool use and tool learning, function calling, code as action
- planning and reasoning for agents (ReAct, plan-and-execute, tree search, reflection, Reflexion-style learning)
- multi-agent coordination, delegation and communication
- agent memory, state and context management
- agent evaluation and benchmarks with methodological contribution
- agent security: prompt injection, permissions, sandboxing, isolation
- human-in-the-loop control of agents

## Exclude filters
- reinforcement-learning agents with no language model, robotics control, game-theoretic multi-agent RL
- domain applications with no transferable architectural idea (unless clearly `topic/domain-applications` material worth a slot)
- leaderboard-only benchmark updates, position papers with no evidence
- papers already filed by af-corpus-papers
- low-quality opinion pieces
- duplicates of existing source notes

## Priority
1. Papers with released code or from established labs and venues
2. Papers that bear on agent-factory's research questions (see `99_Meta/agent-factory/af-targets.md`)
3. Surveys only when no survey on the same subject is in the vault
