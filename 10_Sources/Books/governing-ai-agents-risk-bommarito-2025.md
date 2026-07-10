---
type: source
status: draft
created: 2026-07-10
title: "Agents Part III: Governing AI Agents: Risk, Compliance, and Accountability in Law and Finance"
authors:
- Jillian Bommarito
- Daniel Martin Katz
- Michael J Bommarito II
organisation:
source_type: book
venue: "Working draft chapter, Artificial Intelligence for Law and Finance (forthcoming textbook)"
url: https://github.com/mjbommar/ai-law-finance-book/
year: 2025
date_published: 2025-12-12
anthropic: false
topic:
- topic/security
- topic/domain-applications
tags: [governance, compliance, risk, accountability, regulation]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Agents Part III: Governing AI Agents: Risk, Compliance, and Accountability in Law and Finance

> Full citation: Bommarito, J., Katz, D.M. and Bommarito II, M.J. "Agents Part III: Governing AI Agents: Risk, Compliance, and Accountability in Law and Finance." Working draft chapter, Artificial Intelligence for Law and Finance, 2025. https://github.com/mjbommar/ai-law-finance-book/

## Summary

This chapter is the third part of a textbook trilogy on AI agents for law and finance. Part I defines what makes a system agentic; Part II covers how to build one; this chapter addresses how to govern one responsibly. It targets chief risk officers, compliance officers, general counsel, and senior leadership who must approve, monitor, and improve agentic deployments in regulated domains. The chapter builds on Part I's GPA+IAT taxonomy (Goal, Perception, Action, Iteration, Adaptation, Termination) and argues these six properties map to specific governance requirements. Its central thesis holds that agentic systems differ from passive software in kind, not degree, because an agent interprets what a user wants rather than simply executing instructions. This interpretive gap creates three accountability challenges: purpose drift, perceptual opacity, and actuation risk. A second thesis anchors the law and finance framing: professional duties cannot be delegated to AI. Attorneys, investment advisers, and auditors remain fully liable for AI-assisted work product, so governance functions as the operational mechanism for meeting non-delegable professional duties rather than an optional add-on.

## Key Concepts

- GPA+IAT framework: the six defining properties of agentic systems, used as a requirements map linking each property to a specific governance control.
- Dimensional calibration: governance scales to risk rather than applying uniformly; controls are calibrated across four dimensions.
- Autonomy spectrum (HITL, HOTL, HIC): human-in-the-loop, human-on-the-loop, and human-in-command modes of oversight.
- Entity frame typology: human, hybrid, machine, and institutional framings of how a system presents itself to users.
- Goal dynamics typology: static, adaptive, and negotiated objectives, each with escalating governance burden.
- Persistence: stateless versus stateful systems, with stateful systems carrying compounding error risk.
- The autonomy-auditability trade-off: as autonomy rises, governance shifts from ex-ante approval to ex-post logging and monitoring.
- The five-layer governance framework: foundational law, professional and ethical obligations, sector-specific regulation, AI-specific regulation, and voluntary governance frameworks, applied cumulatively.

## Terminology

- **Human-in-the-Loop (HITL)**: the system recommends actions, but a human must approve before execution. Key risk is automation bias, where reviewers rubber-stamp without meaningful review.
- **Human-on-the-Loop (HOTL)**: the system operates autonomously within defined parameters; humans monitor performance and intervene on anomalies.
- **Human-in-Command (HIC)**: the system operates with high autonomy; humans set strategic goals and constraints, monitor aggregate performance, and retain emergency stop authority.
- **Purpose drift**: the risk that an agent pursues unintended objectives when a goal specification is ambiguous, incomplete, or misaligned with actual intent.
- **Perceptual opacity**: the risk that incomplete, biased, or adversarially manipulated perception produces inappropriate actions even where the goal is well specified.
- **Actuation risk**: the risk created because agents take actions that affect their environment, unlike passive tools that only produce output for human review.
- **The five layers**: foundational law, professional and ethical obligations, sector-specific regulation, AI-specific regulation, and voluntary governance frameworks.

## Architecture and Implementation

The chapter frames implementation around a Dimensional Calibration Worksheet that maps combinations of autonomy, entity frame, goal dynamics, and persistence to specific control sets. Worked domain examples anchor the framework: a legal research assistant sits at HITL, human frame, static goals, and stateless persistence as a low-risk reference case; a bank mortgage or credit underwriting system sits at HIC, institutional frame, adaptive goals, and stateful persistence as a high-risk reference case. Section 4 (implementation) covers risk assessment, audit logging, explainability, human oversight workflows, vendor management, and incident response, though this material falls past the pages read for this note. Section 5 covers organisational accountability, including a RACI matrix for operationalising responsibility and liability allocation across vendors, deployers, and professionals.

## Code Examples

Not applicable. This is a governance and legal-risk chapter with no code samples.

## Best Practices

- Calibrate control intensity to four dimensions (autonomy, entity frame, goal dynamics, persistence) rather than applying uniform controls to every agentic system.
- Match oversight mode to consequence and reversibility: use HITL for high-consequence or irreversible actions, HOTL where volume precludes individual review but errors stay detectable, and HIC only in stable, well-understood, high-volume environments.
- Scale logging and monitoring intensity with autonomy. HIC systems need exceptionally detailed logging plus statistical monitoring for fairness, error trends, and drift, alongside a tested emergency stop mechanism.
- Disclose entity frame transparently. Hybrid-frame deployments should document which tasks are AI-performed versus human-performed.
- Govern adaptive goals by defining which aspects may change, which constraints are inviolable, and what triggers revalidation, while keeping rollback capability available.
- Govern negotiated goals through senior-leadership approval authority, with documented rationale, evidence, and consequences for any proposed change.
- Protect state integrity in stateful systems through comprehensive logging, monitoring for error compounding, and clear state-reset criteria.
- Layer multiple governance frameworks rather than relying on one, since no single framework covers every obligation. The EU AI Act does not address the Equal Credit Opportunity Act's principal-reasons standard, and the NIST AI RMF does not address attorney-client privilege or auditor independence.
- Treat demonstrated reasonable care, through risk assessment, validation, monitoring, and incident response, as the primary defence against liability exposure created by vendor risk-shifting.

## Warnings and Anti-Patterns

- Automation bias: the central risk of HITL governance, where human reviewers rubber-stamp agent recommendations without meaningful scrutiny.
- Entity frame and autonomy mismatch: presenting a high-autonomy HIC system with a human frame leads users to assume oversight that does not exist, creating misplaced trust and liability exposure.
- Institutional frame without institutional oversight: a system deployed by a team without executive approval exposes the organisation to liability for decisions it never authorised.
- Goal drift within adaptive systems: adaptive goals can drift within permitted boundaries, and subtle drift may escape notice until it causes harm.
- Error compounding in stateful systems: a misunderstanding in one session can propagate through subsequent decisions, corrupting an entire chain of reasoning. A financial planning chatbot that misreads a client's risk tolerance in the first session illustrates the pattern.
- Adversarial manipulation of perception through prompt injection, data poisoning, or adversarial examples.
- Runaway execution: an agent taking actions too quickly or too frequently, absent rate limits and circuit breakers.
- Inadequate human review under GDPR Article 22 for stateful agentic systems. Generic guidance to "add a button for human review" is insufficient, since meaningful intervention requires access to the system's accumulated internal state, which demands comprehensive state logging.
- Vendor liability shifting: vendor contracts typically cap damages at the subscription fee through liability caps, warranty disclaimers, and indemnification clauses, an amount often insufficient to cover regulatory penalties or class action settlements.
- Disparate impact in AI credit scoring: a model that disproportionately harms protected classes exposes the lender to fair-lending liability regardless of whether the model was purchased from a reputable vendor.
- Mata v. Avianca, Inc., 678 F. Supp. 3d 443 (S.D.N.Y. 2023): an attorney submitted a brief with hallucinated case citations generated by ChatGPT. The court sanctioned the attorney, not the AI vendor, because the duty to verify legal research is non-delegable. The chapter notes this tool was not agentic, since it lacked iteration, tool access, and verification loops, and argues that agentic systems with autonomous iteration and actuation demand even greater governance.

## Related Concepts

- [[evaluation]]
- [[what-is-an-ai-agent]]
- [[agent-vs-llm]]
- [[what-is-an-agent-bommarito-2025]]
- [[how-to-design-an-agent-bommarito-2025]]

## Future Work

The chapter flags a forthcoming companion volume covering broader AI governance beyond agentic systems, including foundation model evaluation, training data provenance, and non-agentic classifiers. Within this chapter, sections on audit logging, explainability, vendor management, performance monitoring, incident response, RACI-based accountability, liability allocation, and domain-specific worked examples for legal and accounting practice extend beyond the pages reviewed for this note and warrant a follow-up read.

## References

- Mata v. Avianca, Inc., 678 F. Supp. 3d 443 (S.D.N.Y. 2023)
- American Bar Association, Standing Committee on Ethics and Professional Responsibility (2024)
- ABA Model Rules of Professional Conduct, Rule 1.1, Rule 1.6, Rule 3.3
- Equal Credit Opportunity Act
- Investment Advisers Act of 1940
- EU AI Act (2024)
- General Data Protection Regulation, Article 22
- Colorado AI Act (2026)
- Federal Reserve SR 11-7
- NIST AI Risk Management Framework
- ISO/IEC 42001
