---
type: source
status: stub
created: 2026-08-13
title: "The AI Agent Handbook: 10 practical hacks to use AI agents for business"
authors: []
organisation: "Google Cloud"
source_type: book
venue: "Google Cloud marketing ebook"
url: TBD
year: TBD
date_published: TBD
anthropic: false
topic:
- topic/best-practices
- topic/deployment
tags: [google-cloud, gemini-enterprise, vendor-collateral, business-use-cases, enterprise-adoption]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
af_targets:
- none
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: cb0501a3e65691493ed52502abb8cc94cd1e2257f53fa5c7727416f6dd46edf5
---

# The AI Agent Handbook: 10 practical hacks to use AI agents for business

> Full citation: Google Cloud. "The AI Agent Handbook: 10 practical hacks to use
> AI agents for business. Work smarter, not harder." Executive foreword by
> Oliver Parker, VP, Global Generative AI GTM, Google Cloud. Year not stated in
> the extract.

## Summary

This 46-page ebook is Google Cloud marketing collateral. It carries no named
author, no technical architecture, and no code. Each of the 10 chapters follows
one template: a business pain scenario, a Google product that removes it, three
sample prompts, and a customer testimonial. The products named are Gemini
Enterprise (which absorbed Google Agentspace), NotebookLM, the Idea Generation
agent, the Deep Research agent, Customer Engagement Suite with Google AI, Gemini
Code Assist, Agent Gallery, Agent Designer, and Vertex AI Agent Builder. The
closing page sells a companion prompt guide. I set `status: stub` on that basis:
the source teaches nothing about how an agent works, and its every claim routes
to a purchase. Its value to this vault is as evidence of vendor framing and as a
list of the enterprise workflows a large vendor markets agents into.

## Key Concepts

- The 10 hacks, with the claim attached to each:
  1. **Effortlessly search for enterprise data**. Gemini Enterprise searches
     across Drive, email, chat, CRM, order management, HRIS, IT ticketing,
     policies, and project trackers from one bar in the Chrome browser.
  2. **Transform complex documents into engaging podcasts**. NotebookLM ingests
     a document set and returns a podcast summary, a pros and cons list, or a
     sentiment report.
  3. **Generate your best ideas in minutes**. The Idea Generation agent runs
     hundreds of agents to produce 1,000 ideas, then self-scores them through
     multi-angle evaluation and ranks the best.
  4. **Consult an expert on anything**. The Deep Research agent builds and runs
     a research plan across hundreds of web sources plus access-controlled
     enterprise data, then writes one report.
  5. **Personalise customer experience at scale with multi-agent AI**. Customer
     Engagement Suite with Google AI combines Conversational Agents, Agent
     Assist, and Conversational Insights across a contact centre.
  6. **Boost marketing engagement and conversion rates**. Gemini Enterprise
     connects to marketing systems for campaign analysis and content
     generation.
  7. **Shorten the sales cycle**. Agents locate playbooks, monitor customer
     requests, rank leads, and de-duplicate CRM records.
  8. **Find a bug in your code and fix it, with just a prompt**. Gemini
     Enterprise and Gemini Code Assist find reusable code and synthesise bug
     reports from across the organisation.
  9. **Simplify onboarding and other HR workflows**. Agents surface policy,
     analyse exit interviews and attrition, and draft personalised learning
     plans.
  10. **Build your own AI agent**. Three entry points by skill level: Agent
      Gallery for ready-made agents, Agent Designer for no-code custom agents,
      and Vertex AI Agent Builder for developers.
- The intended reader is a business buyer or a line manager, not an engineer.
  Every scenario opens in the second person on a bad workday.
- The framing is time recovered, not capability gained. The subtitle states the
  thesis: work smarter, not harder.
- Google Cloud claims agents differ from traditional automation and chatbots by
  executing complete workflows.
- Google Cloud states Gemini Enterprise supports the open Agent2Agent protocol
  for interoperability with agents built on other platforms.

## Terminology

The source defines its product names, not the field's vocabulary.

- **Gemini Enterprise** - the umbrella product that connects data sources,
  pre-built agents, and custom agents. It absorbed Google Agentspace.
- **Agentspace** - the former product name. Testimonials still use it.
- **Pre-built agent** - an agent Google ships inside Gemini Enterprise, such as
  NotebookLM, Idea Generation, or Deep Research.
- **Agent Gallery** - the catalogue of agents available in one business, from
  Google, internal developers, and partners.
- **Agent Designer** - the no-code, chat-based interface for building a custom
  agent on enterprise data.
- **Vertex AI Agent Builder** - the developer surface for extending or writing
  an agent.
- **Agent2Agent protocol** - the open protocol Google Cloud names for
  cross-platform agent interoperability.

## Architecture and Implementation

The source specifies nothing for building. It names connectors (BigQuery,
SharePoint, Jira, ServiceNow, telephony, UCaaS, and CCaaS systems) and one
protocol, and it stops there. Two hints sit in the prose. Hack one credits
Google knowledge graph technology for linking content to users, which places a
[[knowledge-graph]] under enterprise search. Hack four describes the Deep
Research agent using reasoning, planning, and search to execute a custom plan,
which is [[planning-and-reasoning]] under a product name. Neither claim carries
detail a reader could rebuild from.

## Code Examples

The source carries no code. It carries prompt strings, three per chapter,
written for a business user to paste. Examples: "Analyze these exit interviews
and summarize the common reasons cited for attrition last quarter" and "Find and
delete duplicate lead records in our CRM". The second prompt authorises a
destructive write with no review step, and the source flags no guardrail.

## Best Practices

The source states no engineering practice. Two patterns survive extraction as
observations about how a vendor pitches adoption.

- Start from a workflow that already hurts, then name the agent that takes it.
  Every chapter opens on the pain, not the technology.
- Match the build surface to the builder: catalogue, no-code designer, or
  developer platform.

## Warnings and Anti-Patterns

The source names no risk, no failure mode, and no anti-pattern. That silence is
itself the finding. It offers no evaluation method, no cost discussion, no
accuracy caveat, and no human review gate, save one testimonial from Verizon
that calls the product "human in the loop". Read every performance figure as a
Google Cloud claim, not a field result. The load-bearing ones: Gartner's
forecast that 33% of enterprise software applications will include agentic AI by
2028, with agents then making 15% of day-to-day work decisions; a Google
Workspace poll in which 50% of workers report freed time;
and Seattle Children's hospital retrieving clinical pathway information in
seconds against up to 15 minutes by hand.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[supervisor-worker-multi-agent]]
- [[planning-and-reasoning]]
- [[knowledge-graph]]
- [[10_Sources/Blog/anthropic-building-effective-agents|Building Effective Agents]]
- [[10_Sources/Books/agentic-design-patterns-gulli-2025|Agentic Design Patterns]]

For anything this note gestures at, read those two sources instead. Anthropic's
post supplies the workflow and autonomy distinction this handbook collapses.
Gulli supplies the patterns behind the product names.

## Future Work

The source flags no open problem. It closes by selling a companion guide of 100
or more prompts for Gemini Enterprise, scoped by role and industry across HR,
sales, marketing, finance, and legal.

## References

- Gartner (2024). *Intelligent Agents in AI Really Can Work Alone. Here's How.*
- PRNewswire (2024). *New research from Google Workspace and The Harris Poll
  shows rising leaders are embracing AI to drive impact at work.*
- Google Workspace (2024). *Poll uncovers how new and aspiring leaders deepen
  their impact with AI.*
