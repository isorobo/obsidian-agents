---
type: source
status: draft
created: 2026-07-10
title: "Applying Deep Neural Network to Retrieve Relevant Civil Law Articles"
authors:
- Nga Tran Anh Hang
organisation: "University of Evora, Portugal"
source_type: paper
venue: "Proceedings of the Student Research Workshop associated with RANLP 2017"
url: http://doi.org/10.26615/issn.1314-9156.2017_007
year: 2017
date_published: 2017-09-06
anthropic: false
topic:
- topic/domain-applications
- topic/research-papers
tags: [legal-nlp, coliee, information-retrieval, word2vec, legal-tech]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Applying Deep Neural Network to Retrieve Relevant Civil Law Articles

> Full citation: Tran Anh Hang, N. "Applying Deep Neural Network to Retrieve Relevant Civil Law Articles." Proceedings of the Student Research Workshop associated with RANLP 2017, pages 46-48.

## Summary

The paper addresses the legal information retrieval task at the Competition on Legal Information Extraction/Entailment (COLIEE) 2017. The task asks a system to find the civil law articles relevant to a yes/no bar exam question drawn from the Japanese Legal Bar exam corpus. An article counts as relevant when the query sentence can be answered from its meaning, alone or combined with other articles. The author represents each training query-article pair as a feature vector using word2vec, then trains a deep neural network, DL4J, to map these vectors to relevance scores. At test time, the model extracts features from a new query and scores each candidate article, with a higher score signalling greater relevance. The system trained on 600 query-article pairs and tested on 73 unseen queries drawn from the COLIEE 2017 data set. The author also tried expanding articles with words from the articles they reference, but found this expansion confused the ranking and lowered performance, so the final system scores individual articles on their own text.

## Key Concepts

- The COLIEE legal information retrieval task returns civil law articles relevant to a yes/no bar exam query.
- An article is relevant when it, alone or combined with other articles, entails the answer to the query.
- The corpus uses the RITEVAL XML format from the NTCIR project to pair queries with relevant article identifiers.
- Word2vec turns each query-article pair into a feature vector for the neural network.
- DL4J, a deep learning library, maps feature vectors to a relevance score per article.
- Article cross-references exist in Japanese civil law but expanding articles with referenced text degraded ranking performance.

## Terminology

- **COLIEE** — Competition on Legal Information Extraction/Entailment, an annual competition held alongside the International Conference on Artificial Intelligence and Law.
- **RITEVAL format** — a general XML representation from the NTCIR project used to structure query-article test corpora across domains.
- **DL4J** — Deeplearning4j, the neural network library used to train the relevance model.
- **word2vec** — a word embedding method that produces vector representations of words, used here to featurise query-article pairs.
- **Textual entailment** — the relationship the task exploits: a query counts as answered when its meaning is entailed by an article.

## Architecture and Implementation

The pipeline runs in three stages. First, the system identifies informative sentences and keywords in a query using part-of-speech tagging and named entity recognition. Second, it retrieves candidate articles based on the extracted sentences and keywords. Third, it computes a semantic relevance score between the query and each candidate article using vectors from word2vec, and a DL4J neural network trained to map these vectors to a relevance decision. The model returns the article with the highest confidence score as its answer.

## Code Examples

The paper reports no code listings or implementation snippets. It names the tooling, word2vec for feature vectors and DL4J for the neural network, without reproducing configuration or code.

## Best Practices

- Favour individual article text over reference-expanded text when the domain corpus contains dense cross-referencing, since expansion introduced noise in this system.
- Extract informative sentences and keywords through part-of-speech tagging and named entity recognition before retrieval, rather than searching on raw query text.

## Warnings and Anti-Patterns

- Expanding an article with the text of articles it references confused the ranking and produced worse results than scoring articles on their own text.
- Optimising for precision over recall means the system often selects only the single highest-scoring article, even when a question has more than one relevant article, which caps recall by design.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[legal-nlp-introduction-nazarenko-wyner-2017]]

## Future Work

The author identifies a small training corpus as the main limit on performance and proposes three directions: enlarging the training data set, incorporating a dictionary of criminal law terminology, and using EuroVoc, a multilingual thesaurus, as an additional resource.

## References

- Cabrio, E., Cojan, J., Aprosio, A. P., Magnini, B., Lavelli, A., and Gandon, F., 2012. QAKiS: an open domain QA system based on relational patterns. Proceedings of the 2012th International Conference on Posters & Demonstrations Track, Volume 914, pp. 9-12. CEUR-WS.org.
- Bentivogli, L., Clark, P., Dagan, I., Dang, H., and Giampiccolo, D., 2011. The seventh PASCAL recognizing textual entailment challenge, volume 9, pp. 9-12. Proceedings of TAC.
- Azzopardi, L., Girolami, M., and Van Rijsbergen, C. J., 2008. Concept and context in legal information retrieval, volume 10, pp. 3281-3286. JURIX.
- Azzopardi, L., Girolami, M., and Van Rijsbergen, C. J., 2004. Topic based language models for ad hoc information retrieval. Neural Networks, volume 4, Proceedings 2004 IEEE International Joint Conference on IEEE.
