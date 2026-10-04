---
type: source
status: draft
created: 2026-08-13
title: "A Comprehensive Survey of AI-Enabled Techniques for Automated Legal Text Summarization and Citation Grounding in Judicial Applications"
authors:
- Vijay Kumar S B
- Akash Harihar
- Vedanth R
- Sanjana S V
- Ankitha S
organisation: "Malnad College of Engineering"
source_type: paper
venue: "International Journal of Innovative Research in Technology (IJIRT), Volume 12 Issue 6, ISSN 2349-6002, paper ID 186176"
url: TBD
year: 2025
date_published: 2025-11
anthropic: false
topic:
- topic/research-papers
- topic/domain-applications
tags: [legal-summarisation, survey, transformer-models, citation-grounding, rouge, legaltech]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
af_targets:
- none
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: bf4abbe27fba8d818b0ee3b917c854b8b0ddcd9e6e05e5bb61ee6e0aa4e84112
---

# A Comprehensive Survey of AI-Enabled Techniques for Automated Legal Text Summarization and Citation Grounding in Judicial Applications

> Full citation: Vijay Kumar S B, Harihar, A., Vedanth R, Sanjana S V and Ankitha S. "A Comprehensive Survey of AI-Enabled Techniques for Automated Legal Text Summarization and Citation Grounding in Judicial Applications." International Journal of Innovative Research in Technology (IJIRT), Volume 12 Issue 6, November 2025, pages 7654 to 7667. ISSN 2349-6002. Paper ID 186176.

## Summary

This survey maps AI methods for legal text summarisation and citation grounding. It appeared in the International Journal of Innovative Research in Technology, Volume 12 Issue 6, November 2025. IJIRT is a low-barrier venue with no visible peer-review record. Read the paper as a reading list, not as a validated finding. The authors group 58 numbered references into four themes. Those themes are summarisation techniques, retrieval-augmented generation, applied legal NLP tools, and regulation. They trace a line from graph-based extractive ranking, through transformer abstractive models, to retrieval-augmented and citation-aware systems. Four figures rank LexT5, RAG, and CitaLaw above BART and the Gravitational Search Algorithm across five criteria. The paper states no search protocol, no inclusion criteria, and no source for the scores behind those figures. Its own reference list marks eight entries as duplicates of earlier entries. The value sits in the inventory of datasets, model families, and named failure modes, not in the ranking.

## Key Concepts

- Legal summarisation splits into extractive selection of source sentences and abstractive generation of new text.
- Rhetorical roles such as facts, arguments, and decisions give extractive models domain structure to exploit.
- Retrieval-augmented generation and citation-aware training attack the same problem: a generated citation that does not exist.
- Legal fidelity ranks above fluency. A fluent summary that misstates a holding fails the task.
- Multilingual coverage drives much of the recent work. Greek, Urdu, Turkish, Icelandic, Portuguese, Italian, and Chinese corpora each get a study.
- Interpretability carries weight in this domain because a court demands a reasoned basis, not a score.

## Terminology

- **Extractive summarisation**: selection of sentences from the source document, ranked by relevance.
- **Abstractive summarisation**: generation of new sentences that restate the source content.
- **Rhetorical role segmentation**: labelling of judgment sentences by function, such as facts, arguments, or decision.
- **Weak supervision**: training on heuristic labels rather than manual annotation, used by LawSum on Indian Supreme Court judgments.
- **Citation grounding**: linking a generated statement to a verifiable legal authority.
- **Citation hallucination**: a generated reference to an authority that does not exist or does not support the claim.
- **Co-citation similarity**: labelling two cases as similar because they cite the same legal articles.
- **QLoRA**: quantised low-rank adaptation, a fine-tuning method the survey reports for T5 on Indian case law.
- **Prototype memory**: a module that stores recurring legal patterns and cites them to explain a prediction.

## Architecture and Implementation

The survey describes no system of its own. It catalogues the architectures reported in the works it cites.

**Classical and graph-based extractive**

- Graph ranking over sentences with TextRank, PageRank, HITS, and LexRank.
- Metaheuristic optimisation with the Gravitational Search Algorithm. It frames selection as an NP-hard problem over term frequency, sentence position, and similarity. The cited work reports gains over particle swarm optimisation, genetic algorithms, and TextRank. The cost is parameter tuning and compute.
- Integer linear programming over rhetorical roles, reported to beat 11 baselines on Indian Supreme Court judgments.

**Neural extractive**

- Sequence-to-sequence models with attention.
- Contextual embedding ensembles: BERT variants produce sentence representations, multi-layer perceptrons score relevance, and the outputs combine.
- Reinforcement learning with MemSum on U.S. court opinions, where performance drops at higher compression rates.

**Transformer abstractive**

- General models fine-tuned on legal text: T5, BART, PEGASUS, Legal Pegasus, Longformer, and BERT encoder-decoder pairs.
- Domain-adapted models: LexT5, trained alongside the LexSumm benchmark, and LawGPT for Chinese law.
- Multilingual models: mBART and mT5 for Urdu, mT5 reported at ROUGE-1 of 0.7889.
- Parameter-efficient fine-tuning: BERT extractive filtering feeds a T5 model tuned with QLoRA. The cited work reports ROUGE-1 of 46.37% on Indian case law.
- Two-stage pipelines: sentence-level extractive filtering ahead of a summarisation layer.
- Preprocessing: rule-based text normalisation before BART and PEGASUS, reported to raise output quality on noisy judgments.
- Alignment: supervised fine-tuning, RLHF, and direct preference optimisation on Icelandic legal corpora.

**Retrieval and citation grounding**

- RAG over legal vector stores joined to a Neo4j knowledge graph, presented at ICAIL 2025.
- CitaLaw: citation-aware training objectives plus post-generation citation verification.
- Citation prediction benchmarked on Australian law, with SaulLM and hybrid re-ranking. Best systems sit around 50% below human standard.
- Prototype-based interpretability for citation prediction, which trades some accuracy for an auditable explanation.
- LangChain pipelines that chain retrieval, prompt templates, and generation.

**Datasets and corpora named**

| Resource | Scope |
|---|---|
| LawSum | Indian Supreme Court judgments, weakly supervised |
| LexSumm | Multi-jurisdiction summarisation benchmark, paired with LexT5 |
| CLERC | Over 1.8 million annotated U.S. federal case documents for retrieval and RAG |
| MultiLegalPile | Statutes, treaties, and case law across eight G8 languages |
| LAWSUIT | Expert-written summaries of Italian Constitutional Court cases |
| Australian citation benchmark | Curated set for LLM citation prediction |
| Taiwanese labour law set | Co-citation similarity labelling |
| Indian Constitution sections | Open-source legal language modelling |

Single-language studies cover Greek, Urdu, Turkish, Icelandic, and Portuguese case law. The survey records that Greek and Turkish work lacks a standard dataset.

**Evaluation metrics**

- ROUGE dominates. Reported ROUGE-1 figures: 46.37% for T5 with QLoRA, 0.7889 for mT5 on Urdu, 0.538 for a BART and T5 tool.
- METEOR appears once, at 0.338 for the same hybrid tool.
- Human and expert judgement supplements ROUGE in the two-stage summariser and the MemSum study.
- The survey's own four figures score models on legal domain suitability, language adaptability, accuracy, explainability, and computational efficiency. It supplies no rubric and no data source for these scores.

## Code Examples

The survey ships no code. It cites three public repositories: a LangChain legal summariser, an NLP legal classifier, and the CLERC dataset.

## Best Practices

- Filter extractively before you generate. Two reported pipelines cut the document with BERT or a sentence ranker. They hand the residue to T5.
- Normalise the text before the model sees it. Rule-based cleanup of legal judgments raised BART and PEGASUS output quality in the cited study.
- Fine-tune on domain text. Every comparison in the survey puts a legal-adapted model ahead of the general-purpose equivalent.
- Verify citations after generation. CitaLaw pairs citation-aware training with a post-hoc check rather than trusting the decoder.
- Report the dataset and the model version. The survey marks several entries as irreproducible for omitting both.
- Pair an automated metric with expert review. ROUGE alone does not detect a misstated holding.

## Warnings and Anti-Patterns

- Do not read the survey's model ranking as measurement. The figures give no rubric, no scale, and no provenance for their scores. A pie chart of "percentage accuracy share" across eight models describes nothing measurable.
- Do not treat the reference list as clean. Entries 51 to 58 duplicate entries 34 to 40, as the paper itself records. The numbering around entry 28 is broken.
- Do not trust an unverified LLM citation in a filing. The survey cites the 2025 Reuters report on fabricated citations in court documents.
- Do not assume cross-jurisdiction transfer. Most cited systems serve one court, one language, or one corpus. The authors flag this limit each time.
- Do not equate co-citation with legal similarity. Shared citations proxy relevance; they miss the reasoning.
- Do not deploy without checking the local rule. England permits judicial use of AI for procedural assistance; New South Wales bans AI-generated content in evidence documents.
- Do not push compression. MemSum degrades at higher compression rates, and LexT5 shows faithfulness errors when it compresses detailed argument.

## Related Concepts

- [[retrieval-augmented-generation]]
- [[knowledge-graph]]
- [[evaluation]]
- [[prompt-engineering]]
- [[10_Sources/Papers/legal-nlp-introduction-nazarenko-wyner-2017|Legal NLP Introduction]]
- [[10_Sources/Papers/legal-qa-ranking-svm-cnn-do-2017|Legal QA Ranking with SVM and CNN]]
- [[10_Sources/Papers/legal-text-classification-sulea-2017|Legal Text Classification]]
- [[10_Sources/Papers/civil-law-article-retrieval-tran-2017|Civil Law Article Retrieval]]

## Future Work

The authors flag data scarcity as the binding constraint. They name few annotated corpora, few benchmarks, and no shared evaluation standard. They call for language-agnostic and cross-jurisdictional summarisers, since the reviewed systems each serve one court or one language. Hallucination and citation error stay open, and the survey points to hybrid human and AI review as the current answer. Long input handling remains unsolved for abstractive models. On the governance side, the authors call for interpretable models, bias mitigation, and regulatory oversight before deployment in judicial workflows. They also press for open-access datasets and open reporting, since several works they review withhold model and dataset details.

## References

- Canonical URL: not stated in the extract. IJIRT paper ID 186176, Volume 12 Issue 6, November 2025, pages 7654 to 7667.
- Kanapala, S., Jannu, I. and Pamula, R. "Summarization of Legal Judgments using Gravitational Search Algorithm." Neural Computing and Applications, 2019.
- Parikh, P., Mathur, S., Mehta, P., Mittal, S. and Majumder, P. "LawSum: A Weakly Supervised Approach for Indian Legal Document Summarization." arXiv, 2021.
- Bhattacharya, P., Paul, S., Ghosh, S., Ghosh, S. and Pal, S. "Incorporating Domain Knowledge for Extractive Summarization of Legal Case Documents." arXiv, 2021.
- Shukla, A., Banerjee, S., Rathi, P. and others. "Legal Case Summarization: Extractive and Abstractive Evaluation." arXiv, 2022.
- Bauer, A., Atkinson, B. and others. "Legal Extractive Summarization of U.S. Court Opinions." arXiv, 2023.
- Koniaris, M., Tzitzikas, Y. and Kondylakis, H. "Evaluation of Summarization Techniques for Greek Case Law." MDPI Applied Sciences, 2023.
- Santosh, T. Y. S. S. and others. "LexSumm and LexT5: Benchmarking and Modeling Legal Summarization." arXiv, 2024.
- Barron, M., Eren, O., Serafimova, O., Matuszek, C. and Alexandrov, M. "Bridging Legal Knowledge and AI: Retrieval-Augmented Generation with Vector Stores." ICAIL, 2025.
- Zhang, Y., Yu, T., Dai, L. and Xu, K. "CitaLaw: Enhancing LLM with Citations in Legal Domain." arXiv, 2025.
- Han, J., Burgess, S. and Shareghi, E. "Evaluating LLM-based Approaches to Legal Citation Prediction." arXiv, 2025.
- Hou, J., Luo, Y. and others. "CLERC: A Dataset for Legal Case Retrieval and RAG." 2024.
- Luo, Y., Bhambhoria, P., Dahan, D. and Zhu, H. "Prototype-Based Interpretability for Legal Citation Prediction." arXiv, 2023.
- Niklaus, L., Matoshi, A. and Stürmer, K. "MultiLegalPile: A Multilingual Legal Corpus." ACL, 2024.
- Zhou, L., Shi, Q., Song, D. and Yang, L. "LawGPT: A Chinese Legal Knowledge-Enhanced LLM." 2024.
- Masih, S., Khan, A. and Noor, M. "Transformer-Based Abstractive Summarization of Legal Texts in Low-Resource Languages." MDPI, 2025.
- Akter, M., Çano, E., Weber, E., Dobler, D. and Habernal, I. "A Comprehensive Survey on Legal Summarization: Challenges and Future Directions." 2025.
- Harðarson, G., Loftsson, H. and Ólafsson, S. "Aligning Language Models for Icelandic Legal Text Summarization." arXiv, 2025.
- Albayati, A. and Fındık, B. "Turkish Legal Single-Document Summarization." Springer, 2024.
- Dias, M., Ribeiro, F. and Pinto, A. "Contributions to Legal Document Summarization: Portuguese Supreme Court." Dagstuhl SLATE, 2024.
