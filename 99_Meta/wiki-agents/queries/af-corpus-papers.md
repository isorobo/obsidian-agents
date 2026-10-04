# Query plan - af-corpus-papers

Base surface: see `watchlist.md` channel surface notes. Feeds agent-factory RSCH-01 and RSCH-04 (one-way digest).

## Window
- since_date: 2022-01-01 (seed papers are studied regardless of age; dedupe governs)

## Fetch method
- Seeds: WebFetch `https://arxiv.org/abs/<id>` (or the API `http://export.arxiv.org/api/query?id_list=<id>`). Before writing, confirm the fetched title and first author match the seed line; a mismatch is rejected and flagged.
- After the seeds: arXiv API searches built from the Include keywords, sorted by relevance.

## Seed list (in order; question numbers refer to `99_Meta/agent-factory/af-targets.md`)
1. 2304.03442 Generative Agents: Interactive Simulacra of Human Behavior (Park et al. 2023). RSCH-01; Q11, Q12, Q09.
2. 2309.02427 Cognitive Architectures for Language Agents, CoALA (Sumers et al. 2023). Q01, Q03, Q11, Q30, Q31.
3. 2405.15793 SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering (Yang et al. 2024). Q13, Q14, Q16.
4. 2402.01030 Executable Code Actions Elicit Better LLM Agents, CodeAct (Wang et al. 2024). Q14, Q16.
5. 2310.08560 MemGPT: Towards LLMs as Operating Systems (Packer et al. 2023). Q09, Q11, Q12.
6. 2503.18813 Defeating Prompt Injections by Design, CaMeL (Debenedetti et al. 2025). Q07, Q23, Q26.
7. 2503.13657 Why Do Multi-Agent LLM Systems Fail? (Cemri et al. 2025). Q17, Q24, Q25.
8. 2406.12045 tau-bench: A Benchmark for Tool-Agent-User Interaction in Real-World Domains (Yao et al. 2024). Q18, Q20.
9. 2308.03688 AgentBench: Evaluating LLMs as Agents (Liu et al. 2023). Q20.
10. 2302.04761 Toolformer: Language Models Can Teach Themselves to Use Tools (Schick et al. 2023). Q15, Q16.
11. 2302.12173 Not What You've Signed Up For: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection (Greshake et al. 2023). Q23, Q26.
12. 2406.13352 AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents (Debenedetti et al. 2024). Q20, Q23.
13. 2303.17580 HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face (Shen et al. 2023). Q17, Q29.
14. 2303.17651 Self-Refine: Iterative Refinement with Self-Feedback (Madaan et al. 2023). DELEG-03; Q31.
15. 2310.04406 Language Agent Tree Search Unifies Reasoning, Acting, and Planning in Language Models (Zhou et al. 2023). Q31.
16. 2305.10601 Tree of Thoughts: Deliberate Problem Solving with Large Language Models (Yao et al. 2023). Q31.

## Include filters
- the seed list above
- then: agent architecture papers that bear on the 33 questions: agent definitions and taxonomies; durable state, checkpointing and resumption; memory versus context; observation and action spaces; capabilities and permissions; delegation, sub-agents and communication; budgets and resource control; human approval in the loop; evaluation and evidence of success; runtime and model substitution

## Exclude filters
- papers already in the vault (ReAct, Reflexion, Voyager, AutoGen, CAMEL, AgentVerse, Self-Discover and the surveys) and papers filed by arxiv-agents
- papers without an architectural contribution (pure prompting tricks, leaderboard updates)
- low-quality opinion pieces
- duplicates of existing source notes

## Priority
1. Seed list in order
2. Papers on questions with no supporting note in the latest digest's RSCH-04 coverage
