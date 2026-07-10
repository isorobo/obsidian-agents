---
type: source
status: draft
created: 2026-07-11
title: "Deploy AI Agents to Production (AI Agents 101, Part 5)"
authors:
- Jason Zhou
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 1.8
url: https://www.aibuilderclub.com/blog/ai-agents-101-part-5
year: 2026
date_published: 2026-06-02
anthropic: false
topic:
- topic/deployment
tags:
- deployment
- observability
- cost-controls
- course
nlm_id:
nlm_skip: false
watchlist_channel:
---

# Deploy AI Agents to Production (AI Agents 101, Part 5)

> Jason Zhou, "Deploy AI Agents to Production (AI Agents 101, Part 5)", AI Builder Club, Build AI Agents Course, 2 June 2026 (updated 11 June 2026), https://www.aibuilderclub.com/blog/ai-agents-101-part-5.

## Summary

The closing lesson of the series argues agents fail standard deployment practice in three specific ways — unbounded execution time, non-deterministic per-call cost, and opaque failures that look complete while producing garbage — and walks through containerisation, VPS-versus-serverless choice, structured logging, real health checks, and three-level cost control sufficient to run a monitored production agent for $30 to $40 a month.

## Key Concepts

- Agents violate three standard web-service assumptions: bounded latency, deterministic cost, and legible failure modes.
- A VPS suits agents running over 60 seconds or on a schedule; serverless suits short, webhook-triggered tasks under about a minute.
- Real health checks verify dependencies (model API reachability, memory store connectivity, disk space), not merely process liveness.
- Cost control needs three independent layers: a per-run token budget, a daily spend tracker, and a provider-side dashboard hard limit as the final backstop.

## Terminology

- Structured logging — JSON-formatted log lines with consistent fields, enabling queryable, filterable production auditing of agent decisions, not just errors.
- Health check — an endpoint that verifies both process liveness and the functioning of the agent's actual dependencies.
- Token budget — a hard ceiling on cumulative LLM tokens per agent run, raised as an exception when exceeded.

## Architecture and Implementation

The Dockerfile pins the Python base image and every dependency version explicitly — the lesson states a minor SDK version bump has broken production agents before — installs system dependencies in a separate cached layer, runs as a non-root user, and declares a `HEALTHCHECK`. Deployment favours a fixed-cost VPS (Hetzner CX22, roughly $5 to $8 a month) run with `--restart unless-stopped` for baseline crash recovery over serverless when a task runs long or on a schedule. Logging uses `structlog` for JSON output, binding a `run_id`, `user_id`, and truncated task per run, and logs every step of the loop: run start and completion, LLM call start and response with token counts, and tool call start, completion, and failure. The `/health` endpoint checks model-API reachability, memory-store connectivity, and free disk space, returning `healthy`, `degraded`, or `unhealthy`; a separate `/ping` endpoint serves as a fast liveness probe for the load balancer. Cost control layers a per-run token budget that raises `TokenBudgetExceeded`, a thread-safe daily spend tracker written to disk against a hard daily-dollar limit, and a provider dashboard limit set at roughly twice expected monthly spend as the final backstop.

## Code Examples

The lesson provides a full Dockerfile, a `docker run` command with `--restart unless-stopped`, a `structlog`-based `run_agent_with_logging()` wrapper, a FastAPI `HealthResponse` model and `/health`/`/ping` endpoints, a `Docker HEALTHCHECK` directive, and a daily spend-tracking script with a worked cost calculation (50k prompt tokens plus 15k completion tokens at stated per-token rates equals $0.275).

## Best Practices

- Pin every dependency version; never deploy against "latest".
- Log decisions and reasoning at every step, not only errors.
- Separate liveness (`/ping`) from readiness (`/health`) so a load balancer and a real dependency check answer different questions.
- Layer cost control three deep: per-run budget, daily tracker, and provider hard limit.
- Run the container as a non-root user and keep secrets in environment variables only.

## Warnings and Anti-Patterns

- A single bug — an infinite loop, a malformed tool response, one user request that fans out to a hundred sub-tasks — can generate hundreds of dollars in cost overnight without a token budget.
- An agent lacking a `max_steps` guard has no upper bound on its own execution.
- Deployments consistently blowing past the target monthly budget are, per the lesson, always missing the per-run token budget specifically.

## Related Concepts

- [[the-agent-loop]]
- [[evaluation]]
- [[claude-code]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

This lesson closes the five-part AI Agents 101 series; the course continues into Karpathy commentary on agentic engineering practice.

## References

- Deploy AI Agents to Production (AI Agents 101, Part 5) — https://www.aibuilderclub.com/blog/ai-agents-101-part-5
