---
type: source
status: draft
created: 2026-07-10
title: "VizoMem: A Visual-Textual Memory Framework for Efficient Long-Horizon Reasoning"
authors:
- Weijie Liang
- Yuanfeng Song
- Xing Chen
- Caleb Chen Cao
- Sirui Han
- Yike Guo
organisation: ByteDance and The Hong Kong University of Science and Technology
source_type: paper
venue: Findings of the Association for Computational Linguistics, ACL 2026
url: https://aclanthology.org/2026.findings-acl.365/
year: 2026
date_published: 2026-07-02
anthropic: false
topic:
- topic/memory
- topic/research-papers
tags: [memory, visual-compression, long-context, retrieval, agentic-memory]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# VizoMem: A Visual-Textual Memory Framework for Efficient Long-Horizon Reasoning

> Full citation: Weijie Liang, Yuanfeng Song, Xing Chen, Caleb Chen Cao, Sirui Han, Yike Guo. "VizoMem: A Visual-Textual Memory Framework for Efficient Long-Horizon Reasoning." Findings of the Association for Computational Linguistics, ACL 2026. https://aclanthology.org/2026.findings-acl.365/

## Summary

Long-horizon agents lose accuracy and speed once textual memory outgrows the context window. VizoMem addresses this by pre-rendering textual memories into images and storing them as "visual notes", the fundamental unit of an agentic memory system. Rendering text to a page image achieves a 3-4x token reduction over raw text, following the compression ratio established by Glyph. VizoMem extends that static compression idea into an active, retrievable memory: a dedicated retrieval model, ColGlyph, encodes both queries and rendered memory images with a late-interaction scoring function, so the agent retrieves relevant visual notes without reconstructing long text sequences. An alignment mechanism cross-checks each note's visual and textual embeddings and penalises retrieval scores where the two disagree, guarding against information loss introduced by rendering. Across LoCoMo and LongMemEval, VizoMem's two agent variants match or approach the accuracy of text-based memory baselines such as MIRIX while consuming a fraction of the tokens, for example 4,612 tokens against MIRIX's 18,803 tokens for a comparable overall score on LoCoMo.

## Key Concepts

- Text rendered to a page image compresses 3-4x in token count while preserving the information the task needs.
- A visual note is the fundamental memory unit: an image rendered from a textual memory passage.
- ColGlyph is a dedicated retrieval model for text-rendered images, built on the Glyph vision-language backbone with a ColPali-style late-interaction scorer.
- An alignment score penalises retrieval when a note's visual and textual embeddings disagree, catching rendering-induced information loss.
- Two agent variants trade complexity for accuracy: Direct Visual Retrieval renders whole sessions as images; Visual Hierarchical Memory routes content into six specialised memory types before rendering.

## Terminology

- **VizoMem** - the overall framework that renders textual agent memory as images for compact, agentic long-term memory.
- **Visual Notes** - image-rendered units of textual memory content, the fundamental memory unit in VizoMem.
- **ColGlyph** - the paper's retrieval embedding model for text-rendered images, built on the Glyph backbone with a late-interaction multi-vector scorer and an MLP projection head.
- **GraphMARCO** - the training dataset built for ColGlyph, derived from MS MARCO v1.1, with passages rendered into images.
- **DVR (Direct Visual Retrieval)** - the simpler agent variant: each session renders as one image, retrieved by a fixed count with no structured memory management.
- **ViHM (Visual Hierarchical Memory)** - the MIRIX-inspired agent variant, using six memory agents (Core, Episodic, Resource, Procedural, Semantic, Knowledge Vault) plus a Meta Manager, enhanced with rendered visual content.
- **Alignment Score** - a confidence measure comparing a memory's textual and visual embeddings, used to modulate retrieval scores.
- **MaxSim / late-interaction scoring** - the multi-vector retrieval function inherited from ColBERT and ColPali: the sum, over query tokens, of the maximum similarity to any passage token.
- **Meta Manager** - the routing agent that decides which memory module should process new information.

## Architecture and Implementation

VizoMem sits on three pillars: interaction, memory management, and visual hierarchical memory. The agent interacts with its environment, and new information is rendered and stored as a visual note, or a textual query triggers retrieval. Both notes and queries pass through ColGlyph, whose embeddings reach a meta memory manager that dispatches updates or retrieval requests to the relevant memory agents.

Rendering follows a fixed pipeline inherited from Glyph: page size 595x842, 96 DPI, 10px margins, Verdana 9pt, black text on a white background, left-aligned, with automatic cropping. The rendered image then passes through a vision-language model. Plain Glyph compression alone still hits a ceiling; VizoMem adds agentic memory management on top so it can organise and retrieve contexts far longer than a single render can hold.

ColGlyph reuses the Glyph vision and language towers and adds a single-layer MLP projection head that maps token-level hidden states into a low-dimensional embedding space. Retrieval scores a query against a candidate image with MaxSim: for each query token, take the highest similarity to any passage token, then sum across query tokens. Training uses in-batch negative sampling with cross-entropy loss over the batch similarity matrix, fine-tuning the language tower with LoRA (rank 16) on the q, k, v, and o_proj layers while keeping the vision tower frozen. The 74,089-instance GraphMARCO dataset, built from MS MARCO v1.1, supplies query-positive-negative triples with passages rendered as images.

The alignment mechanism compares a note's textual embedding against its visual embedding using two directional similarity scores, then combines them into a single alignment score. The final retrieval score multiplies the base MaxSim score by this alignment score raised to a tunable exponent (0.5 in the reported experiments), suppressing notes where rendering has introduced a mismatch between what the text says and what the image shows.

Two agent variants implement this architecture. DVR renders each conversation session as a single image and retrieves a fixed number of images per query, with no structured memory management. ViHM, built for the more demanding LoCoMo benchmark, routes new information through a Meta Manager into six specialised memory agents, each updating its own memory state through a two-step extraction-then-update process, where the update operation is one of INSERT, REPLACE, MERGE, or SKIP.

## Code Examples

No code listings appear in the extracted paper text. The paper describes formulae and rendering parameters rather than source code; see Architecture and Implementation above for the equations and configuration values reported.

## Best Practices

- Use a dedicated retrieval encoder for rendered text rather than a general-purpose image encoder. ColGlyph outperforms ColPali-style baselines such as ColQwen2.5 on text-rendered images specifically because it is tuned for that visual domain.
- Cross-check visual and textual embeddings before trusting a retrieved memory. The alignment mechanism catches cases where rendering has degraded or distorted the underlying text.
- Match agent complexity to task demands. DVR's unstructured session rendering wins on single-hop questions where no summarisation is needed; ViHM's structured memory wins on multi-hop questions that require linking facts across sessions.
- Keep DPI and image size within a tested range. Larger images and lower DPI both widen the gap between visual and textual embeddings, so the alignment step becomes more important at lower resolution.

## Warnings and Anti-Patterns

- Visual compression alone does not replace structured memory operations. Organising, updating, and coordinating memory types still needs text-based schemas or LLM-invoked tools, so integrating vision-based memory adds system complexity rather than removing it.
- Over-abstraction in hierarchical memory can cause hallucination. ViHM's summarisation step, in the reported case studies, inferred a fabricated detail (an occupation) that the source text did not support.
- Vague or low-confidence details can vanish during memory evolution. A rendered note carrying an imprecise temporal reference was dropped as low-importance during a later memory update.
- Compression does not remove the underlying context-window ceiling. A 1.3-million-word document still yields around 600,000 visual tokens after 3-4x compression, which exceeds a 128K-token VLM window.
- Multi-step reasoning across chained visual retrievals can accumulate errors, so results on some benchmarks match rather than exceed text-only baselines, a limitation the authors attribute to current vision-language models rather than to the visual modality itself.

## Related Concepts

- [[memory]]
- [[the-agent-loop]]

## Future Work

The authors name three open directions. First, integrating vision-based memory into structured memory operations such as organising, updating, and coordinating memory types remains unresolved, since these operations still depend on text-based schemas or tool calls. Second, the current work stays text-centric, rendering only text-derived images; a general-purpose multimodal architecture that natively handles images, audio, and video is left for future research. Third, the paper relies on LLM-as-a-Judge for its primary evaluation, which may introduce bias or variance despite cross-checks against automatic metrics such as BLEU, ROUGE, and SBERT; the authors call for more robust evaluation protocols.

## References

- Glyph (Cheng et al., 2025) - the vision-language backbone and rendering configuration VizoMem builds on, establishing the 3-4x text-to-image compression ratio.
- ColPali (Faysse et al., 2025) - the late-interaction multi-vector retrieval architecture that ColGlyph adapts for text-rendered images.
- MIRIX (Wang and Chen, 2025) - the six-memory-type hierarchical architecture that ViHM extends with rendered visual content.
- A-MEM (Xu et al., 2025) - a Zettelkasten-inspired agentic memory baseline using temporal evolution and interlinked notes.
- MemOS (Li et al., 2025d) - a memory system storing state as KV-cache, compared as a baseline.
- Mem0 (Chhikara et al., 2025) and Zep (Rasmussen et al., 2025) - token-level agentic memory baselines.
- DeepSeek-OCR (Wei et al., 2025) - introduces Contextual Optical Compression, rendering text into images to compress context.
- LoCoMo (Maharana et al., 2024) and LongMemEval (Wu et al., 2025) - the two long-horizon conversational benchmarks used for evaluation.
- MS MARCO v1.1 (Nguyen et al., 2017) - source corpus for GraphMARCO, the dataset built to train ColGlyph.
