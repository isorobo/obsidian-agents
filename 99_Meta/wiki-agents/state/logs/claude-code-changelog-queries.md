# Query log - claude-code-changelog

## Run 2026-10-04 - Round 1

### Queries issued
1. `https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md` - WebFetch (200, newest version 2.1.289)
2. `https://api.github.com/repos/anthropics/claude-code/releases?per_page=30` - WebFetch (200, returned only 2.1.286 to 2.1.289)
3. `https://api.github.com/repos/anthropics/claude-code/releases/tags/v2.1.285` - WebFetch (200, published 2026-09-29)
4. `https://registry.npmjs.org/@anthropic-ai/claude-code` - WebFetch (200, summary lacked 2.1.x times, not used)

### Candidates
| Title | URL | Date | Outcome |
|---|---|---|---|
| Claude Code 2.1.285 | https://github.com/anthropics/claude-code/releases/tag/v2.1.285 | 2026-09-29 | Accepted |
| Claude Code 2.1.286 | https://github.com/anthropics/claude-code/releases/tag/v2.1.286 | 2026-09-30 | Accepted |
| Claude Code 2.1.287 | https://github.com/anthropics/claude-code/releases/tag/v2.1.287 | 2026-10-01 | Accepted |
| Claude Code 2.1.288 | https://github.com/anthropics/claude-code/releases/tag/v2.1.288 | 2026-10-02 | Accepted |
| Claude Code 2.1.289 | https://github.com/anthropics/claude-code/releases/tag/v2.1.289 | 2026-10-03 | Accepted |

## Run 2026-10-04 - Exit summary

Rounds: 1. Added: 5. Rejected: 0. Exit reason: target met (first run takes the newest CAP versions only).
