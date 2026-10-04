---
type: source
status: draft
created: 2026-10-04
title: "Anthropic Sandbox Runtime (srt)"
authors:
- Anthropic
organisation: Anthropic
source_type: repo
venue: GitHub
url: https://github.com/anthropics/sandbox-runtime
year: 2025
date_published: 2025-10-20
anthropic: true
topic:
- topic/security
- topic/deployment
tags:
- sandboxing
- filesystem-isolation
- network-proxy
- srt
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-github
af_targets:
- af:ADR-0004
- af:RSCH-04/Q23
- cf:ADR-0008
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: ab538c9cf7a18650e938d205b7bf0958d7bac5cb4b8ab860e3cb9eb281848748
---

# Anthropic Sandbox Runtime (srt)

> Anthropic, "Anthropic Sandbox Runtime (srt)", GitHub (anthropics), repository created 20 October 2025, https://github.com/anthropics/sandbox-runtime.

## Summary

A lightweight, OS-level sandbox that restricts filesystem and network access for arbitrary processes without containers. It targets AI agents, MCP servers and local commands. It uses `sandbox-exec` on macOS, `bubblewrap` on Linux and `srt-win` on Windows (alpha), plus HTTP and SOCKS5 proxies on the host that mediate all network traffic. The design is secure by default: a process starts with minimal access and capabilities are granted explicitly. The README calls it a beta research preview for Claude Code, so APIs may change.

## Key Concepts

- Reads are allowed everywhere by default, with deny-then-allow regions (`denyRead`, `allowRead`; allow wins).
- Writes are denied by default, with `allowWrite` and a `denyWrite` that wins inside allowed regions.
- Network is allow-only through domain allowlists and denylists, with wildcards and port suffixes.
- Mandatory write protections cover shell configs, git config and hooks, IDE folders and `.claude/commands/` and `.claude/agents/`.
- Violations are monitored in real time.

## Terminology

- srt: the CLI name for the sandbox runtime.
- SandboxManager: the TypeScript library entry point.
- DNS rebinding check: resolved-address checking so an allowed domain cannot map to a blocked address.

## Architecture and Implementation

On Linux, network traffic reaches host proxies over bind-mounted Unix sockets. On macOS, Seatbelt profiles limit communication to specific localhost ports. On Windows, a dedicated account, WFP filters and NTFS ACLs apply. A `--control-fd` option allows live network rule changes. Settings live in `~/.srt-settings.json`.

## Code Examples

```bash
srt "curl example.com"
srt --debug "npm install"
srt --settings custom.json "bash"
```

```typescript
import { SandboxManager } from '@anthropic-ai/sandbox-runtime'
await SandboxManager.initialize(config)
const wrapped = await SandboxManager.wrapWithSandbox('npm test')
await SandboxManager.reset()
```

## Best Practices

- Start from no access and add only what the task needs.
- Deny sensitive reads such as `~/.ssh` and write-protect `.env` and `.git/hooks`.
- Wrap MCP servers in the sandbox as well as the agent's shell.

## Warnings and Anti-Patterns

- Domain allowlists do not inspect traffic, so an allowed domain such as GitHub can still carry exfiltrated data.
- Allowing `/var/run/docker.sock` gives effective host access.
- Broad write access to `$PATH` or shell configs enables privilege escalation.
- `enableWeakerNestedSandbox`, `enableWeakerNetworkIsolation` and `allowAppleEvents` weaken isolation.
- Environment-variable proxies can be ignored by non-compliant applications.

## Related Concepts

- [[claude-code]]
- [[mcp]]
- [[tool-use]]

## Future Work

Windows support is alpha and the whole tool is a research preview.

## References

- https://github.com/anthropics/sandbox-runtime
