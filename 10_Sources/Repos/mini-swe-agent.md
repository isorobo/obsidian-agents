---
type: source
status: draft
created: 2026-10-04
title: "mini-SWE-agent"
authors:
- SWE-agent team
organisation: SWE-agent
source_type: repo
venue: GitHub
url: https://github.com/SWE-agent/mini-swe-agent
year: 2025
date_published: 2025-06-28
anthropic: false
topic:
- topic/architectures
- topic/evaluation
tags:
- mini-swe-agent
- minimal-agent
- bash-only
- swe-bench
nlm_id:
nlm_skip: false
watchlist_channel: af-corpus-repos
af_targets:
- af:RSCH-01/mini-swe-agent
- af:ADR-0001
- af:RSCH-04/Q01
- af:RSCH-04/Q16
- af:RSCH-04/Q23
wiki_indexed: '2026-10-04T03:40:46Z'
wiki_hash: 4b2bebf68be7c6987a46ff882bc8c526f0e961c2ad145d095cff725eca5cef20
---

# mini-SWE-agent

> SWE-agent team, "mini-SWE-agent", GitHub, 28 June 2025, https://github.com/SWE-agent/mini-swe-agent.

## Summary

mini-SWE-agent is a deliberately minimal software engineering agent. The authors ask what happens if the agent is 100 times simpler and still works nearly as well. The agent class is about 100 lines, with separate small pieces for the environment, model interface and run script. The README claims over 74 percent on SWE-bench Verified, adoption by several large organisations, faster start-up than Claude Code, and a better result than Claude Code and Codex on DeepSWE (these are the README's own claims, not checked). The repository was created 28 June 2025, last pushed 28 September 2026, MIT licence (GitHub API, this run). This note covers the README only.

## Key Concepts

- Bash is the only tool; the model uses shell commands for file edits, tests and PRs.
- History is completely linear: the trajectory equals the messages sent to the model.
- Each action runs through `subprocess.run` independently, with no persistent shell session.

## Terminology

- Linear history: every step appends to one message list, with no summarising or branching.
- Stateless execution: each command is a fresh subprocess.

## Architecture and Implementation

An agent object takes a model wrapper and an environment. The loop asks the model for a bash action, runs it in the environment, appends the output and repeats. Because actions are independent subprocesses, sandboxing is described as trivial: swap the environment. The linear history makes debugging and fine-tuning on trajectories simple.

## Code Examples

```python
agent = DefaultAgent(
    LitellmModel(model_name=...),
    LocalEnvironment(),
)
agent.run("Write a sudoku game")
```

## Best Practices

- Start with the smallest loop and add machinery only when a result demands it.
- Keep the message list identical to the trajectory so runs are replayable.
- Put isolation in the environment object, not in the agent.

## Warnings and Anti-Patterns

- Large tool schemas and heavy configuration add state without clear gain, by the authors' argument.

## Related Concepts

- [[the-agent-loop]]
- [[tool-use]]
- [[evaluation]]

## Future Work

Core code paths and the docs on why it is minimal are candidates for part notes.

## References

- https://github.com/SWE-agent/mini-swe-agent
