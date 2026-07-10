---
type: source
status: draft
created: 2026-07-10
title: "Voyager: An Open-Ended Embodied Agent with Large Language Models"
authors:
- Guanzhi Wang
- Yuqi Xie
- Yunfan Jiang
- Ajay Mandlekar
- Chaowei Xiao
- Yuke Zhu
- Linxi Fan
- Anima Anandkumar
organisation: NVIDIA
source_type: paper
venue: 
url: https://arxiv.org/abs/2305.16291
year: 2023
date_published: 2023-05-25
anthropic: false
topic:
- topic/architectures
- topic/research-papers
tags: [embodied-agent, skill-library, curriculum, minecraft, code-generation]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Voyager: An Open-Ended Embodied Agent with Large Language Models

> Full citation: Wang, Xie, Jiang, Mandlekar, Xiao, Zhu, Fan, and Anandkumar. "Voyager: An Open-Ended Embodied Agent with Large Language Models." arXiv:2305.16291, 2023. https://arxiv.org/abs/2305.16291

## Summary

Voyager is an LLM-powered agent that plays Minecraft continuously, without a human setting its goals. The authors, working from NVIDIA with co-authors from Caltech, UT Austin, Stanford, and UW Madison, built the agent from three parts: an automatic curriculum that proposes the next task, a skill library that stores verified behaviours as executable code, and an iterative prompting mechanism that repairs generated code using environment feedback, execution errors, and self-verification. Voyager queries GPT-4 as a blackbox, so no fine-tuning occurs. The agent obtains 3.3 times more unique items, travels 2.3 times further, and unlocks tech-tree milestones up to 15.3 times faster than prior state-of-the-art baselines. It is the only tested method that unlocks a diamond tool. The skill library also transfers to a new Minecraft world, letting Voyager solve novel tasks from scratch while other methods fail to generalise.

## Key Concepts

- An automatic curriculum that proposes the next exploration task from the agent's current state.
- A skill library that stores each learned behaviour as an executable code function.
- An iterative prompting loop that refines code using environment feedback, execution errors, and self-verification.
- In-context lifelong learning without gradient updates or fine-tuning.
- Skill compounding, where earlier skills compose into later, more complex ones.

## Terminology

- Automatic curriculum — a GPT-4 component that generates the next task from the agent's inventory, position, and task history.
- Skill library — a vector database keyed by the embedding of a skill's description, valued by its executable code.
- Iterative prompting mechanism — the refinement loop that resubmits code to GPT-4 with feedback until it passes self-verification.
- Environment feedback — a text message from the Minecraft game state, such as a missing crafting ingredient.
- Self-verification — a separate GPT-4 instance that checks task success and critiques a failed attempt.
- Control primitive API — the Mineflayer function set Voyager calls to act in Minecraft.

## Architecture and Implementation

The automatic curriculum drives exploration in a bottom-up fashion. It prompts GPT-4 with the agent's inventory, equipment, nearby blocks and entities, biome, time, health, hunger, and position, alongside a record of completed and failed tasks. The prompt also carries self-asked and self-answered questions that GPT-3.5 generates to keep exploration cheap. The curriculum runs at a higher temperature than the rest of the system to widen task diversity.

The skill library stores each skill as executable JavaScript code that scaffolds a temporally extended action, such as combat routines or crafting sequences. GPT-3.5 embeds each skill's description with `text-embedding-ada-002`; that embedding becomes the key in a vector database, and the code becomes the value. When a new task arrives, GPT-3.5 drafts a general approach, combines it with environment feedback, and retrieves the five closest skills by embedding similarity. Voyager composes those retrieved skills into the next program rather than writing from scratch each time. Verified skills join the library permanently, which compounds ability over time and reduces catastrophic forgetting.

The iterative prompting mechanism closes the loop between code and world. Environment feedback surfaces through `bot.chat()` calls inside the control primitive API, reporting concrete blockers such as a missing ingredient. The program interpreter reports execution errors, including invalid operations and syntax faults. A separate GPT-4 instance performs self-verification, acting as a critic that compares task outcome against the current game state and returns a fix suggestion on failure. The loop repeats until self-verification passes or four rounds elapse, at which point the curriculum issues a new task regardless.

## Code Examples

The authors host a live project page and reference implementation at https://voyager.minedojo.org. Voyager builds on MineDojo and calls the Mineflayer JavaScript API for low-level motor control in Minecraft.

## Best Practices

- Store learned behaviours as executable code, not free text, so skills compose and run deterministically.
- Retrieve a small top-k set of relevant skills rather than replaying the full library on each task.
- Route cheap auxiliary language work, such as embeddings and self-questions, to a smaller model to control cost.
- Cap refinement rounds per task so a stuck loop cannot stall the curriculum indefinitely.

## Warnings and Anti-Patterns

- GPT-4 queries cost roughly 15 times more than GPT-3.5, so unrestricted use of the strongest model raises budget fast.
- Self-verification can misfire on ambiguous success signals, for example failing to recognise a dropped item as proof of a kill.
- The curriculum can hallucinate items that do not exist in the game, such as a non-existent alloy tool.
- Code generation can hallucinate invalid actions or call undefined API functions, which the execution-error channel must catch.

## Related Concepts

- [[the-agent-loop]]
- [[tool-use]]
- [[memory]]
- [[planning-and-reasoning]]

## Future Work

The authors name three open problems. Cost remains high because GPT-4 is far more expensive than GPT-3.5, though its code quality justifies the expense over cheaper models. Inaccuracies persist, since the agent sometimes stalls on the correct skill and self-verification occasionally misjudges success. Hallucination affects both the curriculum, which can propose nonexistent items, and code generation, which can invoke undefined functions or misuse game objects. The authors expect stronger GPT models and fine-tuned open-source LLMs to narrow these gaps.

## References

- https://arxiv.org/abs/2305.16291
- Project page and code: https://voyager.minedojo.org
