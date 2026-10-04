# Query log - anthropic-github

## Run 2026-10-04 - Round 1

### Queries issued
1. `https://api.github.com/orgs/anthropics/repos?per_page=100&sort=pushed` - WebFetch (200, list truncated after 17 repos)
2. `https://api.github.com/repos/anthropics/claude-agent-sdk-python/releases?per_page=10` - WebFetch (200)
3. `https://api.github.com/repos/anthropics/claude-agent-sdk-typescript/releases?per_page=10` - WebFetch (200)
4. READMEs via raw.githubusercontent.com for claude-agent-sdk-python, claude-agent-sdk-typescript, commerce-agents, sandbox-runtime, claude-code-action, skills - WebFetch (200)

### Candidates
| Title | URL | Date | Outcome |
|---|---|---|---|
| Claude Agent SDK for Python | https://github.com/anthropics/claude-agent-sdk-python | 2025-06-11 | Accepted |
| Claude Agent SDK for TypeScript | https://github.com/anthropics/claude-agent-sdk-typescript | 2025-09-27 | Accepted |
| Claude Commerce Agents | https://github.com/anthropics/commerce-agents | 2026-09-01 | Accepted |
| Anthropic Sandbox Runtime (srt) | https://github.com/anthropics/sandbox-runtime | 2025-10-20 | Accepted |
| Claude Code Action | https://github.com/anthropics/claude-code-action | 2025-05-19 | Accepted |
| Anthropic Agent Skills Repository | https://github.com/anthropics/skills | 2025-09-22 | Accepted |
| claude-code | https://github.com/anthropics/claude-code | 2026-10-03 | Not pursued - belongs to claude-code-changelog |
| knowledge-work-plugins, claude-plugins-official | https://github.com/anthropics/knowledge-work-plugins | 2026-10-03 | Not pursued - target met with stronger items |
| SDK releases (python v0.2.153-163, ts v0.3.280-289) | https://github.com/anthropics/claude-agent-sdk-python/releases | 2026-09/10 | Not pursued - target met with stronger items |

## Run 2026-10-04 - Exit summary
Rounds 1, added 6, rejected 0, exit: target met. Note: state and notes were written in one batch, so the per-note checkpoint was collapsed into a single state write.
