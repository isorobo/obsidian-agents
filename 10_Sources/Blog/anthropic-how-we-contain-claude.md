---
type: source
status: draft
created: 2026-10-04
title: "How we contain Claude across products"
authors:
- Max McGuinness
- Mikaela Grace
- Jiri De Jonghe
- Jake Eaton
- Abel Ribbink
organisation: Anthropic
source_type: blog
venue: Anthropic Engineering
url: https://www.anthropic.com/engineering/how-we-contain-claude
year: 2026
date_published: 2026-05-25
anthropic: true
topic:
- topic/security
- topic/claude-code
- topic/best-practices
tags:
- containment
- sandboxing
- prompt-injection
- approval-fatigue
- egress-controls
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-engineering
af_targets:
- af:RSCH-04/Q23
- af:ADR-0004
- af:ADR-0007
- af:RSCH-04/Q28
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: fd64ab2ac37e24b2ad1e70fca4024e03597ef39b2876c13e77e8826f8cff30fe
---

# How we contain Claude across products

> Max McGuinness, Mikaela Grace, Jiri De Jonghe, Jake Eaton and Abel Ribbink, "How we contain Claude across products", Anthropic Engineering, 25 May 2026, https://www.anthropic.com/engineering/how-we-contain-claude.

## Summary

The post frames containment as an engineering problem: the more capable an agent is, the larger the damage from a failure. Anthropic compares two approaches, human-in-the-loop approval and environmental containment, and reports that users approved about 93% of permission prompts, which is approval fatigue. The authors argue that the deterministic boundary is what holds when probabilistic model defences miss, so containment is designed at the environment layer first and the model layer second. They describe three deployed patterns (ephemeral server-side container for claude.ai, human-in-the-loop sandbox for Claude Code, local VM for Claude Cowork) and the failures each exposed. Page access was via the primary page; figures are as reported there.

## Key Concepts

- Three defended components: the environment (sandboxes, VMs, filesystem boundaries, egress controls), the model (system prompts, classifiers, probes, training) and external content (MCP servers, plugins, web search).
- Environmental controls are deterministic; model defences shape tendencies but are probabilistic.
- Match isolation strength to the user's capacity to supervise: developers can review bash, knowledge workers need stricter automatic enforcement.
- An audited connector is not audited data: a trusted tool can still return poisoned content.
- Allowlists are capability grants, so a broad allowed domain can become an exfiltration path.

## Terminology

- Blast radius: the theoretical maximum damage from agent misbehaviour.
- Approval fatigue: users approving prompts without real review.
- Egress controls: network boundaries that stop data leaving.
- Canary string: an embedded marker used to detect unauthorised access to protected content.
- gVisor: a user-space Linux kernel implementation used for container sandboxing.

## Architecture and Implementation

- Ephemeral container (claude.ai): server-side gVisor containers with a per-session filesystem. Small blast radius, lower capability ceiling. Custom proxy components proved weaker than established primitives.
- Human-in-the-loop sandbox (Claude Code): runs on the user's machine with OS-level sandboxing. Approval fatigue led to an automated auto mode, reported as catching about 83% of risky behaviours. Missed cases: project configuration (hooks in `.claude/settings.json`) parsed before the trust prompt, and a phishing-style request to read cloud credentials that succeeded in 24 of 25 attempts.
- Local VM (Claude Cowork): platform hypervisors isolate the code execution, the workspace is mounted over vsock, credentials stay in the host keychain and the agent loop runs outside the VM. Two controls sit outside the guest kernel and four inside. A missed case was exfiltration through an allowlisted domain using an attacker-supplied API key, fixed with a proxy inside the VM that validates session tokens.
- Isolation blocks endpoint detection tooling, so monitoring uses pull-based OTLP exports.

## Code Examples

The source carries no reusable code. It points to the open-sourced Claude Code sandbox runtime for auditability.

## Best Practices

- Design containment at the environment layer first.
- Defer all project-local configuration parsing until after trust is accepted; treat project open like an untrusted network request.
- Treat local input (config files, hooks, localhost listeners) as untrusted.
- Scan tool output with the same rigour as external files.
- Prefer battle-tested primitives (hypervisors, seccomp, gVisor) over custom security components.
- Plan endpoint visibility requirements early when using VMs.

## Warnings and Anti-Patterns

- Parsing configuration before the trust dialog lets hooks run without consent.
- Relying on the model to refuse when the user is the injection vector.
- Allowlisting a broad domain without validating which credentials traffic uses.
- Custom proxies were a weak point in all three deployments.

## Related Concepts

- [[claude-code]]
- [[tool-use]]
- [[mcp]]
- [[best-practices-index]]

## Future Work

The authors flag persistent memory poisoning, multi-agent trust escalation (treating sub-agent output as more trusted than raw tool results) and unresolved agent identity (distinct principals versus inherited user permissions).

## References

- https://www.anthropic.com/engineering/how-we-contain-claude
- Claude Code sandbox runtime: https://github.com/anthropic-experimental/sandbox-runtime
