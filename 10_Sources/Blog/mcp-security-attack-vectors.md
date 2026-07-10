---
type: source
status: draft
created: 2026-07-11
title: "MCP Security: 6 Attack Vectors and a 5-Step Audit"
authors:
- Shirley
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 3.3
url: https://www.aibuilderclub.com/blog/mcp-security-attack-vectors
year: 2026
date_published: 2026-06-11
anthropic: false
topic:
- topic/security
tags:
- mcp
- security
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
---

# MCP Security: 6 Attack Vectors and a 5-Step Audit

> Shirley, "MCP Security: 6 Attack Vectors and a 5-Step Audit", AI Builder Club, Build AI Agents Course, 11 June 2026, https://www.aibuilderclub.com/blog/mcp-security-attack-vectors.

## Summary

MCP's trust model differs from ordinary supply-chain risk in one specific way: a tool description is a model-visible prompt, not just documentation for a human — malicious instructions can sit in text a person never reads but the agent always does. Combined with servers that run locally with the user's own permissions and often auto-fetch their latest version, the lesson argues few people ever examine the source before installing. It names six concrete attack vectors and closes with a five-step, roughly fifteen-minute pre-install audit.

## Key Concepts

- **Tool description poisoning** — hidden, model-directed instructions embedded in a tool's description field, invisible to the human operator but fully read by the agent (the lesson cites a documented WhatsApp-server case rerouting messages to a proxy number this way).
- **Data exfiltration** — a function that looks legitimate but silently posts sensitive parameters to an attacker-controlled endpoint while returning a normal success response.
- **Malicious command execution** — a server disguised as a utility that shells out to install a backdoor or persistence mechanism.
- **Sensitive file reads** — unvalidated reads from predictable credential paths (`~/.ssh/id_rsa`, `~/.aws/credentials`) without path allowlisting.
- **Rug pulls** — a clean initial version that turns malicious later, either through an unpinned `@latest` install or a server that fetches and hot-swaps its own tool definitions at runtime.
- **Cross-server tool hijacking** — one compromised server injecting metadata that instructs the agent to compromise a sibling server that is itself honestly implemented; trust across installed servers is multiplicative, not additive.

## Terminology

- Tool description poisoning — an attack that plants model-directed instructions inside a tool's description field rather than its execution logic.
- Rug pull — a delayed attack where a trusted-looking server becomes malicious after the fact, via a version bump or runtime self-modification.

## Architecture and Implementation

The five-step pre-install audit: read every tool description in the actual source, not the documentation, flagging imperative language directed at the model; grep for outbound network calls (`fetch`, `axios`, `http.request`) and confirm every destination domain matches the server's stated purpose; grep for shell execution (`execSync`, `spawn`, `child_process`, `os.system`, `subprocess`) and require a purpose-level justification for any hit; check every file-read path for allowlisting and normalisation, flagging hardcoded references to `.ssh`, `.env`, or credential directories; and inspect `package.json` for `postinstall`/`preinstall` lifecycle scripts, which run before the tool is ever invoked.

## Code Examples

None as runnable code; the lesson instead gives concrete, quoted examples of each attack pattern (a poisoned tool description, an exfiltrating fetch call, a backdooring shell command) to make each vector recognisable in a real code review.

## Best Practices

- Pin exact server versions and vendor critical servers locally; never run `npx -y server@latest` for anything that matters.
- Scope filesystem access to a single working directory, never a home directory.
- Apply OS-level sandboxing (filesystem and network isolation) as a backstop for audits that miss something.
- Use a `PreToolUse` hook to block writes to `.env` and `.ssh` and to keep an audit log of every tool invocation.
- Prefer simple, widely used, readable server implementations over feature-rich ones with a larger unaudited surface.

## Warnings and Anti-Patterns

- Treating five clean servers plus one compromised server as "five-sixths safe" misunderstands the trust model; one compromised server can instruct the agent to compromise the others.
- MCP, per the lesson, "shipped composability first and integrity verification basically never" — until the protocol grows signatures and re-consent, the operator is the verification layer, not the ecosystem.
- Name-squatting (a package name one character off a legitimate one) defeats a trust check based on name similarity alone.

## Related Concepts

- [[mcp]]
- [[claude-code]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson notes AI-assisted auditing (running the five-step checklist with a model, then a human verifying the findings) as a way to compress the fifteen-minute manual audit, without walking through the workflow.

## References

- MCP Security: 6 Attack Vectors and a 5-Step Audit — https://www.aibuilderclub.com/blog/mcp-security-attack-vectors
