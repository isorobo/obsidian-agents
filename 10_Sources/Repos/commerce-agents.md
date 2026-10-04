---
type: source
status: draft
created: 2026-10-04
title: "Claude Commerce Agents"
authors:
- Anthropic
organisation: Anthropic
source_type: repo
venue: GitHub
url: https://github.com/anthropics/commerce-agents
year: 2026
date_published: 2026-09-01
anthropic: true
topic:
- topic/domain-applications
- topic/best-practices
tags:
- commerce
- reference-implementation
- approval-gate
- managed-agents
nlm_id:
nlm_skip: false
watchlist_channel: anthropic-github
af_targets:
- af:ADR-0007
- af:ADR-0004
- af:RSCH-04/Q28
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: f41a923f1fac192ccfb513311b9127da23f60fa6191b8256f6fe618c2ebaccf7
---

# Claude Commerce Agents

> Anthropic, "Claude Commerce Agents", GitHub (anthropics), repository created 1 September 2026, https://github.com/anthropics/commerce-agents.

## Summary

A reference blueprint for building shopping and merchant agents with Claude. It ships two agents: a customer-facing shopping agent (search, comparison, cart, order tracking, policy questions, conversation memory) and a staff-facing merchant agent (analytics, catalogue and listing edits, inventory and pricing actions, campaign drafts). The same prompts, skills and tool contracts run on three paths: a Messages API reference loop, the Agent SDK, and Managed Agents with MCP. The README says it is a reference implementation, is not maintained and does not take contributions. Licence is Apache 2.0.

## Key Concepts

- One agent definition, three runtimes: prompts, skills and tool contracts are shared.
- Five skill flows per agent, kept in `skills/` directories.
- Backends sit behind `StorefrontBackend` and `MerchantBackend` interfaces that the adopter maps to their own systems.
- Safety lives inside the tool call, so it holds on every runtime path: fencing, provenance gates, caps, memory validation and the merchant approval gate.
- No MCP connectors ship with the project; official connectors are named only as integration targets.

## Terminology

- Staged change: a merchant write held until a person approves it.
- Provenance gate: a check on where data in a tool result came from.
- Vertical: one of retail, travel, telecom and entertainment demo configurations.

## Architecture and Implementation

Agents call backend methods through tools. Enforcement is in the tool layer rather than the prompt. Checkout renders the cart for the host application to complete. Rules are documented in `docs/safety.md`, which was not fetched here.

## Code Examples

```bash
git clone https://github.com/anthropics/commerce-agents.git
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env  # add ANTHROPIC_API_KEY
python scripts/run_demo.py retail
```

## Best Practices

- Put approval and caps inside the tool call so every runtime path inherits them.
- Stage consequential writes for human approval.
- Keep skills and tool contracts identical across runtimes.

## Warnings and Anti-Patterns

- The README says nothing places an order, charges a card or changes a live listing; adopters must not assume otherwise without building those paths.
- Unmaintained: treat as a pattern to copy, not a dependency.

## Related Concepts

- [[claude-agent-sdk]]
- [[tool-use]]
- [[workflow-vs-autonomous-agent]]

## Future Work

None stated; the project is declared unmaintained.

## References

- https://github.com/anthropics/commerce-agents
