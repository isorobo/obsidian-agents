---
type: source
status: draft
created: 2026-10-04
title: "Agent Sandboxes: OS-Level Security for AI Agents (2026)"
authors:
- Shirley
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club - Build AI Agents Course, Section 4.2
url: https://www.aibuilderclub.com/blog/agent-sandbox-os-level-security
year: 2026
date_published: 2026-06-11
anthropic: false
topic:
- topic/security
- topic/deployment
tags:
- sandbox
- bubblewrap
- seatbelt
- prompt-injection
- isolation
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
af_targets:
- af:ADR-0004
- af:RSCH-04/Q23
- af:RSCH-04/Q26
- af:ADR-0007
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: db6c9607e08513a654cff48754a191aa17ad8017881ba7a4d3728ea11c07440d
---

# Agent Sandboxes: OS-Level Security for AI Agents (2026)

> Shirley, "Agent Sandboxes: OS-Level Security for AI Agents (2026)", AI Builder Club, Build AI Agents Course, 11 June 2026, https://www.aibuilderclub.com/blog/agent-sandbox-os-level-security.

## Summary

Agents run with the user's permissions, so a successful prompt injection inherits them. Per-command approval causes approval fatigue. The lesson proposes a two-wall sandbox, filesystem and network isolation together, enforced in the OS kernel rather than the application. Its framing: the sandbox does not detect attacks, it makes their payloads unexecutable. It gives an isolation ladder and five ways teams defeat their own sandbox.

## Key Concepts

- Filesystem wall: write only to the project directory, broad reads with sensitive paths excluded.
- Network wall: all traffic through a proxy with a domain allowlist.
- Kernel enforcement: Seatbelt on macOS, bubblewrap on Linux and WSL2, nothing on WSL1.
- Isolation ladder: Docker (trusted code), bwrap or Seatbelt (personal agents, default), gVisor (multi-tenant, 10 to 30 percent I/O cost), Firecracker (about 125 ms boot, untrusted code as a service).
- Permission modes calibrate trust, hooks encode rules, the sandbox is the floor.

## Terminology

- Approval fatigue: users click through repeated prompts without reading.
- Namespace: the Linux isolation mechanism bwrap uses; unlisted paths simply do not exist.
- Exfiltration: unauthorised data extraction.

## Architecture and Implementation

Example attacks and outcomes: appending to `~/.bashrc` is denied; posting environment variables to an unlisted domain is rejected by the proxy; reading `~/.ssh/id_rsa` fails under bwrap because the path is absent; a malicious `npm postinstall` runs but is confined. Settings named: `dangerouslyDisableSandbox` (per-command escape hatch), `allowUnsandboxedCommands: false`, `sandbox.failIfUnavailable: true`, `sandbox.filesystem.allowWrite`.

## Code Examples

The source carries no reusable code beyond the setting names above.

## Best Practices

- Fence the yard once, then stop asking.
- Block by domain, not port.
- Make sandbox startup failure fatal.
- Treat capability and permission as separate axes.

## Warnings and Anti-Patterns

- Building one wall and skipping the other.
- Wildcard allowlists such as `*.github.com`, which include attacker-controlled pages.
- Writable `$PATH` directories.
- Silent degradation when the sandbox fails.
- Passing through Unix sockets such as the Docker socket, which is root-equivalent.

## Related Concepts

- [[claude-code]]
- [[tool-use]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson mentions `@anthropic-ai/sandbox-runtime` as an open-source implementation to adopt.

## References

- Agent Sandboxes: https://www.aibuilderclub.com/blog/agent-sandbox-os-level-security
- Cited by the lesson: gVisor docs (https://gvisor.dev/docs/), Firecracker (https://firecracker-microvm.github.io/).
