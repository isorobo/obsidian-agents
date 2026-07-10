---
type: source
status: draft
created: 2026-07-10
title: "Agents Part I: What is an Agent? A Conceptual Primer and History"
authors:
- Michael J Bommarito II
- Jillian Bommarito
- Daniel Martin Katz
organisation: 
source_type: book
venue: "Working draft chapter, Artificial Intelligence for Law and Finance (forthcoming textbook)"
url: https://github.com/mjbommar/ai-law-finance-book/
year: 2025
date_published: 2025-11-25
anthropic: false
topic:
- topic/foundations
- topic/domain-applications
tags: [agent-taxonomy, legal-ai, primer, history, agency-law]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Agents Part I: What is an Agent? A Conceptual Primer and History

> Full citation: Bommarito II, M.J., Bommarito, J. and Katz, D.M. "Agents Part I: What is an Agent? A Conceptual Primer and History." Working draft chapter, Artificial Intelligence for Law and Finance, 2025. https://github.com/mjbommar/ai-law-finance-book/

## Summary

The chapter builds a formal definition of "agent" from the ground up, then traces the concept across seven decades. It opens with an intuitive framing, agents as "doers" with a to-do, and formalises this into a three-level nested hierarchy. Level 1 sets minimal agency: an entity that pursues goals through perception and action, with discretion over its response, summarised by the mnemonic GPA (Goal, Perception, Action). Level 2 and Level 3 define an "agentic system", a goal-directed agent that repeatedly perceives and acts, adapting from observations until clear termination conditions are met, summarised as GPA+IAT (adding Iteration, Adaptation, Termination). Level 2 systems implement these six properties through rules or algorithms; Level 3 systems implement the same properties through AI or machine learning, particularly large language models. The property set stays constant across levels; only the implementation mechanism changes. The historical section, "A Historical Journey: Defining Agents Across Seven Decades", starts from the Latin root *agō* and moves through Roman and mercantile agency law, the American Law Institute's Restatements of Agency, mid-century philosophy of action (Anscombe, Davidson), and social and economic theory of the 1970s and 1980s (Milgram, Jensen and Meckling, Giddens, Minsky, Bratman, Dennett, Bandura), before a timeline figure carries the story into the 1990s computer science revolution and the 2020s large language model era. The chapter opens with *Mata v. Avianca* (2023), the fabricated-citations case, as the motivating example for a law and finance audience, and argues that professional deployment needs four safeguards beyond the six operational properties: attribution, provenance, escalation, and confidentiality.

## Key Concepts

- Level 1 agency requires goals, perception, and action, with discretion over the response (GPA).
- An "agentic system" adds iteration, adaptation, and termination to the base three properties (GPA+IAT).
- Level 2 and Level 3 agentic systems share identical properties and differ only in mechanism: rules and algorithms against AI and machine learning.
- Professional deployment in law and finance needs four extra safeguards beyond the six operational properties: attribution, provenance, escalation, and confidentiality.
- The concept of "agent" has a continuous lineage from Roman agency law through mid-century philosophy of action to present-day artificial intelligence.

## Terminology

- **Agent** — an entity that pursues goals through perception and action, with at least minimal discretion over which action to take in response to what it perceives. Requires three properties (GPA).
- **Agentic system** — a goal-directed agent that repeatedly perceives and acts in its environment, adapting from observations until clear termination conditions are met. Requires six properties (GPA+IAT).
- **Agentic software** — a Level 2 agentic system implemented through rules or algorithms rather than AI or machine learning.
- **Agentic AI / AI agent** — a Level 3 agentic system implemented through AI or machine learning, particularly large language models.
- **Falsification test** — the chapter's method for each property: a stated criterion that excludes systems lacking that property, for example a compiler fails the Goals test because it transforms inputs mechanically, without reference to a success criterion.

## Architecture and Implementation

The chapter presents a nested hierarchy rather than a system architecture: Agent (Level 1) sits inside Agentic Software (Level 2), which sits inside Agentic AI (Level 3), set out in Figure 1. A six-question evaluation rubric operationalises the GPA+IAT properties, each paired with domain examples and a falsification criterion. A four-tier spectrum table separates systems into Not Agents, Agents with Incomplete Properties, Full Agents-Traditional, and Full Agents-AI-Powered. A companion table ties terminology to property count: three properties earns the label "agent"; six earns "agentic system"; six delivered through AI or machine learning earns "agentic AI"; four or five properties earns a qualified label such as "agent with..."; one or two properties should use "tool", "function", or "classifier" instead of "agent".

## Code Examples

This is a conceptual chapter; it does not ship code.

## Best Practices

The chapter sets out five common misconceptions to guard against when labelling a system an agent: a single-shot response, automation alone, tool use alone, complexity alone, and AI-poweredness alone are each independently insufficient for agency. For professional deployment in law and finance, the authors add four safeguards beyond the six operational properties: attribution (who or what is responsible for an action), provenance (where an input or output came from), escalation (when a human must intervene), and confidentiality (protection of privileged or sensitive information).

## Warnings and Anti-Patterns

The chapter opens with *Mata v. Avianca, Inc.* (2023), the case in which a lawyer submitted a court filing citing fabricated cases generated by ChatGPT, as a cautionary example of the stakes in professional agent deployment. It warns against loose use of the term "agent" for systems that lack the full property set, and against treating tool use, automation, or AI-poweredness as sufficient grounds for the label on their own.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[agent-vs-llm]]
- [[the-agent-loop]]
- [[workflow-vs-autonomous-agent]]
- [[how-to-design-an-agent-bommarito-2025]]
- [[governing-ai-agents-risk-bommarito-2025]]

## Future Work

The chapter's later sections, beyond the pages read for this note, extend the historical timeline through the 1990s computer science revolution, a period of consolidation and formalisation from the late 1990s to 2019, and the large language model era from 2020 to 2025. Planned further sections cover disciplinary perspectives from philosophy, psychology, law, economics, cognitive science, complex systems, and computer science, analytical dimensions such as the autonomy spectrum, entity frames, goal dynamics, and persistence and embodiment, and a closing analytical framework covering the formal core, boundary cases, and professional deployment.

## References

- Anscombe, G.E.M. *Intention*. 1957.
- American Law Institute. *Restatement (Second) of Agency*. 1958.
- Davidson, D. "Actions, Reasons, and Causes." 1963.
- Coase, R. "The Nature of the Firm." 1937.
- Milgram, S. *Obedience to Authority*. 1974.
- Jensen, M.C. and Meckling, W.H. "Theory of the Firm: Managerial Behavior, Agency Costs and Ownership Structure." 1976.
- Giddens, A. Structuration theory. 1984.
- Minsky, M. *Society of Mind*. 1986.
- Bratman, M. *Intention, Plans, and Practical Reason*. 1987.
- Dennett, D. *The Intentional Stance*. 1987.
- Bandura, A. Human agency theory. 1989.
- Lewis, C.T. and Short, C. *A Latin Dictionary*. 1879.
- Russell, S. and Norvig, P. *Artificial Intelligence: A Modern Approach*. 2020.
- *Mata v. Avianca, Inc.*, 2023.
