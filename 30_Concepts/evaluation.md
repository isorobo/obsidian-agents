---
type: concept
status: draft
created: 2026-07-10
name: Evaluation
slug: evaluation
topic:
- topic/evaluation
tags: [evals, testing, monitoring]
synonyms: [evals, agent evaluation, agent testing]
defined_in: "[[10_Sources/Blog/anthropic-demystifying-evals|Demystifying Evals for AI Agents]]"
related_concepts: ["[[best-practices-index]]", "[[anti-patterns-index]]", "[[the-agent-loop]]"]
anthropic: true
af_targets:
- af:ADR-0008
- af:RSCH-04/Q18
- af:RSCH-04/Q19
- af:RSCH-04/Q20
wiki_indexed: '2026-10-04T03:42:35Z'
wiki_hash: 6f8813c51188dce0ae3aa97a2451b2eaf2e80bf57a1faf44f930d54b0fa3baf8
---

# Evaluation

> Evaluation measures whether an agent does the right thing across a set of representative tasks.

## Summary

Evaluation turns agent quality from opinion into measurement. A team writes eval sets early, runs them on every change, and catches regressions before they compound. Anthropic frames three grader types and a multi-layered method. Code-based graders check outcomes. Model-based graders judge nuance. Human graders set the gold standard. Together they cover what any single method misses.

## Key Concepts

- **Offline eval sets** — A fixed set of tasks with known good outcomes, run before release.
- **LLM-as-judge** — A separate model scores an output against a rubric written in plain language.
- **Trajectory scoring** — A grader reads the full messages array, not just the final answer.
- **Regression suites** — Tasks with a near-100% baseline that guard against quality decline.
- **Guardrails** — A separate model instance screens input and output for policy breaches.
- **Production monitoring** — Live sampling that reveals distribution drift after launch.

## Detail

Start small. Draw 20 to 50 tasks from real failures rather than wait for perfect infrastructure. Convert each user-reported bug into a test case, ranked by impact. Prove each task is solvable with a reference solution, and balance positive and negative cases so optimisation stays honest.

Distinguish two eval types. A regression eval starts near 100% and defends it. A capability eval starts low and climbs, measuring what the agent can newly accomplish. Track pass@k when one success suffices. Track pass^k when every attempt must succeed.

Read the transcripts. The full trajectory shows where a grader measures the wrong thing. Sample transcripts on a schedule to keep model-based graders calibrated against expert consensus.

## Trade-offs and Limits

Code-based graders run fast and stay objective, yet they break on valid variation. Model-based graders capture nuance, yet they drift without calibration. Human graders judge best, yet they cost time and money. A production system combines all three.

## Related

- [[best-practices-index]]
- [[anti-patterns-index]]
- [[the-agent-loop]]
- [[supervisor-worker-multi-agent]]

## Sources

- [[10_Sources/Blog/anthropic-demystifying-evals|Demystifying Evals for AI Agents]] — https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents
- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]] — https://www.anthropic.com/engineering/building-effective-agents
- [[10_Sources/Blog/anthropic-april-23-postmortem|An update on recent Claude Code quality reports]]
- [[10_Sources/Blog/anthropic-eval-awareness-browsecomp|Eval awareness in BrowseComp]]
- [[10_Sources/Blog/anthropic-harness-design-long-running-apps|Harness design for long-running application development]]
- [[10_Sources/Blog/harness-six-components|The 6 Components of a Production Agent Harness]]
- [[10_Sources/Blog/how-to-evaluate-ai-agents|How to Evaluate AI Agents]]
- [[10_Sources/Papers/deny-without-disabling-zhang-2026|Deny Without Disabling (Zhang et al., 2026)]]
- [[10_Sources/Papers/where-multi-agent-systems-fail-han-2026|Where Do Multi-Agent Systems Fail? (Han, 2026)]]
- [[10_Sources/Repos/mini-swe-agent|mini-SWE-agent]]

## See also

- [[MOC - Evaluation]]
