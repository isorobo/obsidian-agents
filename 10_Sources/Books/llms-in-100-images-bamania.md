---
type: source
status: draft
created: 2026-08-13
title: "LLMs in 100 Images"
authors:
- Ashish Bamania
organisation: TBD
source_type: book
venue: TBD
url: TBD
year: TBD
date_published: TBD
anthropic: false
topic:
- topic/foundations
- topic/concepts
tags: [llm-foundations, illustrated-guide, visual-glossary, transformer-architecture, decoding-strategies, alignment-and-rlhf]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
---

# LLMs in 100 Images

> Full citation: Bamania, A. "LLMs in 100 Images". Publisher, year, and ISBN
> absent from the extract. The closing page lists the author's Substack,
> Medium, LinkedIn, and Gumroad store.

## Summary

This book defines 100 large language model concepts, one per numbered page,
each paired with a drawing. Ashish Bamania wrote and illustrated it. The author
opens by stating he selected the concepts after reading hundreds of research
papers. The format is a visual glossary. Each page carries a term, the expanded
acronym, a definition of two or three lines, and a diagram. The sequence runs
from model families, through transformer internals, decoding, measurement,
prompting, retrieval, training, efficiency, and safety. This book sits outside
the vault's agent focus. It is foundational background on the LLM an agent
calls, not agent engineering. Two of the 100 pages touch agents: page 50
defines an AI agent and page 51 defines MCP. Read it to fill gaps on the LLM
side of [[agent-vs-llm]], and read
[[10_Sources/Books/ai-agents-illustrated-guidebook-chawla-pachaar-2025|AI Agents: The Illustrated Guidebook]]
for the agent side.

## Key Concepts

The teaching order groups the 100 pages into 13 blocks.

- Pages 1 to 9 set the landscape: LLM, transformer, GPT, BERT, Llama, large
  reasoning model, multimodal LLM, context window, and Common Crawl.
- Pages 10 to 13 cover input representation: embeddings, byte-pair encoding,
  positional encoding, and rotary position embeddings.
- Pages 14 to 20 cover attention: self-attention, multi-head attention, causal
  masking, flash attention, then the grouped-query, multi-query, and
  multi-head latent variants.
- Pages 21 to 24 cover generation mechanics: inference, autoregression, masked
  language modelling, and key-value caching.
- Pages 25 to 31 cover decoding: softmax, greedy decoding, beam search, top-k
  sampling, top-p sampling, temperature, and test-time scaling.
- Pages 32 to 37 cover measurement: perplexity, BLEU, pass@k, win rate,
  hallucination, and needle-in-a-haystack testing.
- Pages 38 to 47 cover prompting and reasoning: prompt engineering, zero-shot,
  few-shot, chain-of-thought, zero-shot chain-of-thought, chain-of-draft, tree
  of thoughts, ReAct, self-consistency, and self-verification.
- Pages 48 to 53 cover the application layer: vector database, RAG, AI agents,
  MCP, A2A, and LangChain.
- Pages 54 to 57 cover adjacent architectures and one benchmark: CLIP, vision
  transformer, diffusion transformer, and ARC-AGI.
- Pages 58 to 70 cover training machinery: loss function, cross entropy,
  gradient descent, optimiser, and the activation function family from ReLU
  through SwiGLU.
- Pages 71 to 79 cover generalisation: underfitting, overfitting,
  regularisation, L1, L2, dropout, layer normalisation, catastrophic
  forgetting, and concept drift.
- Pages 80 to 91 cover training and post-training: self-supervised learning,
  pretraining, supervised fine-tuning, LoRA, alignment, RLHF, RLAIF, DPO,
  knowledge distillation, PPO, GRPO, and RLVR.
- Pages 92 to 100 cover efficiency and safety: weight pruning, quantisation,
  gradient checkpointing, mixture of experts, Mamba, Constitutional AI, red
  teaming, prompt injection, and prompt moderation.

Three structural points carry across the blocks.

- The attention block reads as one problem and four answers. Multi-head
  attention sets the baseline; grouped-query, multi-query, and multi-head
  latent attention each cut key-value cache cost.
- The reasoning block treats extra computation at inference as the lever.
  Chain-of-thought, tree of thoughts, self-consistency, and test-time scaling
  all trade tokens for accuracy.
- The alignment block traces one lineage. RLHF replaces the human scorer with
  a model in RLAIF, drops reinforcement learning in DPO, and drops subjective
  preference in RLVR.

## Terminology

- **Large reasoning model**: a model built for multi-step reasoning rather than
  language understanding alone.
- **Context window**: the maximum token count a model processes in one prompt
  or conversation.
- **Byte-pair encoding**: a tokenisation method that merges the most frequent
  character pairs into subword units.
- **Rotary position embeddings**: position encoding that rotates query and key
  vectors by an angle set by token position.
- **Causal masking**: blocking a token from attending to any later token.
- **Key-value caching**: storing computed attention keys and values so decoding
  skips repeated work.
- **Test-time scaling**: spending more computation at inference, through longer
  reasoning chains or repeated attempts, to raise accuracy.
- **Pass@k**: the probability that at least one of k generated outputs holds a
  correct solution.
- **Win rate**: the share of pairwise comparisons in which one model's response
  wins the evaluator's preference.
- **Needle-in-a-haystack testing**: hiding a known fact in a long document,
  then querying for it to test long-context retrieval.
- **Chain-of-draft prompting**: step-by-step reasoning capped at a few words
  per step, which cuts output length and keeps the logic.
- **Self-verification**: ranking candidate answers by whether each one
  reconstructs a masked part of the original problem.
- **Catastrophic forgetting**: loss of prior capability after fine-tuning on a
  new task or domain.
- **Concept drift**: change in the data distribution over time, which degrades
  a fixed model's predictions.
- **RLVR**: reinforcement learning against rewards checked against facts or
  logical constraints rather than human preference.
- **Mixture of experts**: an architecture that holds many expert subnetworks
  and routes each token to a few.

## Architecture and Implementation

The book specifies nothing for building. It diagrams architectures and stops
there. The transformer page draws the encoder and decoder stack with
positional encoding, multi-head attention, add-and-norm, feed-forward, and
softmax. The GPT page reduces that to a decoder-only block repeated N times.
The BERT page shows the encoder-only stack with a masked token. Further
diagrams cover the vision transformer patch pipeline, the diffusion
transformer denoising stack, the mixture-of-experts router, and the Mamba
selective state-space block. The RLHF, PPO, GRPO, and Constitutional AI pages
diagram training loops with a policy model, a reward model, and a reference
model. A reader gains vocabulary and a mental picture. A reader gains no
configuration, no parameter values, and no build sequence.

## Code Examples

The book carries no reusable code. One page shows a three-line Python
palindrome function as an illustration of multimodal output. Several pages
carry formulas rather than code: scaled dot-product attention, perplexity,
cross entropy, the L1 and L2 penalty terms, and the ReLU, sigmoid, Swish,
SiLU, and GELU definitions.

## Best Practices

The book states few practices. Four hold across its pages.

- Match the decoding strategy to the need. Greedy decoding gives determinism,
  top-k gives bounded randomness, and top-p adapts the candidate set per step.
- Set temperature low for focused output and high for varied output.
- Spend inference compute on a hard query. The test-time scaling page shows a
  wrong answer from a direct pass and a correct answer after reasoning.
- Test long-context claims with a needle-in-a-haystack run rather than a stated
  token limit.

## Warnings and Anti-Patterns

- Hallucination produces text that reads as plausible and states false facts.
  The worked example dates the Eiffel Tower to 1787.
- Overfitting makes a model memorise training data, including noise, and fail
  on new text.
- Underfitting leaves a model too simple to capture the pattern, and it fails
  on both training and test data.
- Fine-tuning on a narrow domain costs prior capability. The worked example
  shows a medical fine-tune that refuses a translation request.
- Concept drift degrades a fixed model as the world moves.
- Prompt injection overrides system instructions through user input. The worked
  example wraps a refused request in a false emergency and gets an answer.
- BLEU below 10 marks a translation as useless, so a reported score needs its
  band, not its number alone.

## Related Concepts

- [[agent-vs-llm]]
- [[what-is-an-ai-agent]]
- [[prompt-engineering]]
- [[react]]
- [[planning-and-reasoning]]
- [[reflexion]]
- [[retrieval-augmented-generation]]
- [[tool-use]]
- [[evaluation]]
- [[mcp]]
- [[glossary]]

Related sources:

- [[10_Sources/Books/ai-agents-illustrated-guidebook-chawla-pachaar-2025|AI Agents: The Illustrated Guidebook]], which covers the agent layer this book reaches on two pages.
- [[10_Sources/Books/mcp-illustrated-guidebook-chawla-pachaar-2025|MCP: The Illustrated Guidebook]], which expands the single MCP page into a protocol treatment.

## Future Work

The book flags no open problem and proposes no research agenda. It closes on
prompt moderation, then a page of links to the author's channels. The ARC-AGI
page records the nearest thing to an open question: a human panel scores 100%
where the listed models score 4% and 0%.

## References

- The extract names no publisher, no ISBN, and no publication year.
- The closing page lists the author's Substack sites intoai.pub and
  intoquantum.pub, a Medium profile, a LinkedIn profile, and a Gumroad store
  at bamaniaashish.gumroad.com.
- The book cites no papers by name. Concepts trace to their originating work
  through the diagrams alone.
</content>
</invoke>
