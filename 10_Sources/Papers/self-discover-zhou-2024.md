---
type: source
status: draft
created: 2026-07-10
title: "Self-Discover: Large Language Models Self-Compose Reasoning Structures"
authors:
- Pei Zhou
- Jay Pujara
- Xiang Ren
- Xinyun Chen
- Heng-Tze Cheng
- Quoc V. Le
- Ed H. Chi
- Denny Zhou
- Swaroop Mishra
- Huaixiu Steven Zheng
organisation: Google
source_type: paper
venue: 
url: https://arxiv.org/abs/2402.03620
year: 2024
date_published: 2024-02-06
anthropic: false
topic:
- topic/planning
- topic/research-papers
tags: [reasoning, self-composition, prompting, meta-reasoning, structured-reasoning]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Self-Discover: Large Language Models Self-Compose Reasoning Structures

> Full citation: Pei Zhou, Jay Pujara, Xiang Ren, Xinyun Chen, Heng-Tze Cheng, Quoc V. Le, Ed H. Chi, Denny Zhou, Swaroop Mishra, Huaixiu Steven Zheng. "Self-Discover: Large Language Models Self-Compose Reasoning Structures." arXiv, 2024. https://arxiv.org/abs/2402.03620

## Summary

Self-Discover addresses a limit in single-technique prompting methods such as chain-of-thought. Each such method imposes one fixed reasoning process on every task, regardless of the task's actual structure. The authors argue that a task carries its own intrinsic reasoning structure, and that an LLM can uncover that structure before it solves any instance of the task. Self-Discover runs a two-stage process. Stage 1 operates once per task and produces a task-specific reasoning structure, expressed as a JSON-like set of key-value pairs, by selecting, adapting, and implementing a subset of generic reasoning modules such as "critical thinking" or "break the problem into sub-problems." Stage 2 reuses that structure across every instance of the task, prompting the model to fill in each key in turn to reach a final answer. On BIG-Bench Hard, Thinking for Doing, and MATH, Self-Discover outperforms chain-of-thought on 21 of 25 tasks, with gains up to 42% on individual tasks, and outperforms inference-heavy ensemble methods such CoT-Self-Consistency while using 10-40x fewer inference calls, because the discovery step runs once at the task level rather than once per instance. The authors also show the discovered structures transfer across model families, from PaLM 2-L to GPT-4 and from GPT-4 to Llama2, and note that these structures resemble patterns in human problem-solving.

## Key Concepts

- Atomic reasoning modules: short, natural-language descriptions of generic problem-solving heuristics, such as step-by-step thinking or reflective thinking, drawn from a fixed seed set.
- Task-intrinsic reasoning structure: the specific composition of reasoning steps that best fits a given task, distinct from any single a priori method like chain-of-thought.
- Task-level versus instance-level computation: structure discovery runs once per task; solving runs once per instance, which is the source of the method's inference efficiency.
- Self-discovery: the model composes its own reasoning structure from atomic modules rather than following a structure a human designed in advance.

## Terminology

- SELECT: the action that chooses a relevant subset of reasoning modules from the seed set, based on unlabelled task examples.
- ADAPT: the action that rephrases each selected module's generic description into task-specific language.
- IMPLEMENT: the action that converts the adapted descriptions into a concrete, structured plan in key-value format, guided by a human-written demonstration structure for a different task.
- Reasoning structure: the JSON-like output of Stage 1, with keys naming reasoning steps and values filled in during Stage 2 to produce the answer.
- Meta-prompt: a prompt that instructs the model to perform SELECT, ADAPT, or IMPLEMENT, as distinct from the prompt that solves a task instance.

## Architecture and Implementation

Self-Discover splits into two stages. Stage 1 runs three actions in sequence, each driven by its own meta-prompt and the same underlying model.

SELECT takes the full seed set of reasoning module descriptions and a handful of unlabelled task examples, and asks the model to pick the subset relevant to the task. Not every module helps every task, so this step filters the seed set down before further processing.

ADAPT takes the selected subset and rephrases each module from a generic description into one specific to the task at hand. A generic instruction to "break the problem into sub-problems" becomes, for an arithmetic task, an instruction to "calculate each arithmetic operation in order."

IMPLEMENT takes the adapted descriptions and converts them into an actionable structure with explicit fields, formatted as key-value pairs similar to JSON. This step also receives a human-written example structure for an unrelated task, which serves as a demonstration of the target format rather than as task-specific content.

Stage 1 runs once per task, not once per instance, which keeps the extra inference cost to three additional calls regardless of how many instances the task contains. Stage 2 then appends the resulting reasoning structure to every task instance, and the model fills in each key in the structure during decoding to reach the final answer. The authors report that this self-composed, task-specific structure both outperforms fixed methods like chain-of-thought and avoids the repeated-sampling cost of ensemble methods like self-consistency.

## Code Examples

The paper works entirely through prompt design and does not release accompanying code in the text extracted here. The reasoning structure itself functions as a lightweight schema: a set of named keys, such as "Type and colour of each item" or "Number of items of each type," which the model must populate in order during Stage 2 to reach the answer key.

## Best Practices

- Keep the seed set of reasoning modules broad and generic, so SELECT has real options to filter across different task types.
- Run structure discovery once per task rather than per instance, since the paper's efficiency gains depend on treating Stage 1 as a task-level, not instance-level, cost.
- Use a human-written demonstration structure during IMPLEMENT, since the paper found this improved the model's ability to produce a well-formed structured output.
- Format the discovered structure as key-value pairs. The authors tie this format choice to findings elsewhere that structured, JSON-like output improves reasoning and generation quality.

## Warnings and Anti-Patterns

- Do not assume one reasoning method fits all tasks. The paper's central argument is that a priori methods such as chain-of-thought impose a fixed process that does not match every task's intrinsic structure.
- Do not treat ensemble methods such as self-consistency as the default path to higher accuracy. The paper shows Self-Discover reaches better results at a fraction of the inference cost.
- Watch for computation errors on tasks with heavy arithmetic content. The authors report that a majority of failures on MATH come from computation errors rather than structural or planning failures.

## Related Concepts

- [[planning-and-reasoning]]
- [[prompt-engineering]]
- [[plan-and-execute]]

## Future Work

The authors point to further work on structured reasoning for LLMs generally, including deeper study of why self-discovered structures transfer across model families, and closer analysis of where structured reasoning helps most, such as tasks requiring world knowledge versus purely algorithmic tasks.

## References

- Wei et al., "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models," 2022.
- Wang et al., "Self-Consistency Improves Chain of Thought Reasoning in Language Models," 2022.
- Wang et al., "Plan-and-Solve Prompting," 2023.
- Suzgun et al., "Challenging BIG-Bench Tasks and Whether Chain-of-Thought Can Solve Them" (BIG-Bench Hard), 2022.
- Zhou et al., "Least-to-Most Prompting Enables Complex Reasoning in Large Language Models," 2022.
- Hendrycks et al., "Measuring Mathematical Problem Solving With the MATH Dataset," 2021.
- Yang et al., "Large Language Models as Optimizers" (OPRO), 2023.
