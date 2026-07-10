---
type: source
status: draft
created: 2026-07-10
title: "Legal Question Answering Using Ranking SVM and Deep Convolutional Neural Network"
authors:
- Phong-Khac Do
- Huy-Tien Nguyen
- Chien-Xuan Tran
- Minh-Tien Nguyen
- Minh-Le Nguyen
organisation: 
source_type: paper
venue: 
url: https://arxiv.org/abs/1703.05320
year: 2017
date_published: 2017-03-16
anthropic: false
topic:
- topic/domain-applications
- topic/research-papers
tags: [legal-nlp, question-answering, coliee, ranking-svm, convolutional-neural-network]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Legal Question Answering Using Ranking SVM and Deep Convolutional Neural Network

> Full citation: Phong-Khac Do, Huy-Tien Nguyen, Chien-Xuan Tran, Minh-Tien Nguyen, Minh-Le Nguyen. "Legal Question Answering Using Ranking SVM and Deep Convolutional Neural Network." arXiv, 2017. https://arxiv.org/abs/1703.05320

## Summary

This paper builds a two-stage pipeline for the Japanese Civil Code track of the Competition on Legal Information Extraction/Entailment (COLIEE) 2016, which pairs a legal information retrieval task with a yes/no legal question answering task. The retrieval stage trains a Ranking SVM over a triple of similarity features (Latent Semantic Indexing, Manhattan distance, Jaccard distance) to rank candidate civil code articles against a query, operating at paragraph level rather than whole-article level. The authors split each multiple-paragraph article into independent single-paragraph articles, arguing that a query usually matches one paragraph, not an entire article, and this splitting raises the retrieval F1-score from 0.5652 to 0.6087 on their held-out set. The question answering stage feeds a convolutional neural network with word-embedding vectors for the question and its most relevant retrieved sentence, augmented with the TF-IDF and LSI statistical features from the retrieval stage, and classifies each query-article pair as "YES" or "NO". This augmented CNN reaches 57.6% accuracy against 51.5% for a plain CNN. In the COLIEE 2016 formal runs, the combined system (submitted as JNLP3) scored 0.5478 F1 on phase 1 retrieval, close to the second-placed system, but trailed the top systems on phase 2 and phase 3 entailment, which the authors attribute to the CNN's sensitivity to initialisation and to the small size of the legal training set.

## Key Concepts

- Legal information retrieval (LIR) ranks civil code articles against a query using a learning-to-rank model.
- Legal question answering (LQA) treats the yes/no answer as a textual entailment problem between a query and a retrieved article.
- Paragraph-level splitting of multiple-paragraph articles reduces noise in the ranking signal.
- Feature fusion combines classical information-retrieval statistics with a neural sentence encoder.

## Terminology

- **COLIEE** — Competition on Legal Information Extraction/Entailment, the shared task the paper competes in, run alongside the JURISIN workshop.
- **Ranking SVM (SVM-Rank)** — a pairwise learning-to-rank method that optimises a linear scoring function over document pairs.
- **LSI** — Latent Semantic Indexing, a dimensionality reduction of the TF-IDF term-document matrix into a lower-dimensional latent space.
- **Generalised Jaccard similarity** — a Jaccard coefficient computed over TF-IDF weighted vectors rather than binary sets.
- **Textual entailment** — the task of deciding whether the content of one text logically supports or contradicts another, here framed as a binary "YES"/"NO" classification.

## Architecture and Implementation

The pipeline has two trained models. The Ranking SVM takes a query-article feature vector built from LSI, Manhattan distance, and Jaccard distance, and produces a relevance score per candidate article; articles score above 0.85 of the top score are treated as relevant. The CNN takes a 400-dimensional input formed by interleaving 200-dimensional bag-of-words embeddings (Word2Vec, trained on 13.5 million words of Japanese Civil Code text) for the question and for the top-ranked article sentence. Ten convolution filters of length two run over adjacent input pairs, followed by average pooling, and the pooled output is concatenated with TF-IDF and LSI features before a two-layer perceptron produces the final classification. At inference, the framework retrieves the top five articles per question and combines per-article CNN predictions through a voting scheme, testing "no voting", "voting without ratio", and "voting with ratio" variants; unweighted voting performs best at 49.4% accuracy.

## Code Examples

Not applicable. The paper is a systems and experiments report; it does not publish source code or a public repository.

## Best Practices

- Split multi-paragraph legal articles into single-paragraph units before indexing, since a query typically maps to one paragraph rather than a whole article.
- Remove stopwords after lemmatisation, not before, because lemmatisation can turn a non-stopword into a stopword.
- Run neural models with several random initialisations and select against a validation set, since the CNN's accuracy varies by roughly five percentage points across seeds.
- Combine sparse lexical features (TF-IDF, Jaccard) with dense latent features (LSI) rather than relying on either alone, since the leave-one-out feature study shows Jaccard drives most of the Ranking SVM's performance.

## Warnings and Anti-Patterns

- Expanding an article's text with the content of articles it references degrades ranking performance, since referenced text tends to be noisy relative to the query.
- A deep CNN can overfit quickly on a small legal training set (412 query-article pairs), so added statistical features and careful initialisation matter more than architecture depth here.
- High-dimensional sparse TF-IDF vectors fed directly into a CNN inflate the parameter count and worsen overfitting compared with a lower-dimensional LSI representation.

## Related Concepts

- [[evaluation]] — COLIEE functions as a domain-specific evaluation benchmark, and the paper's ablation tables illustrate feature- and component-level evaluation practice for a legal NLP pipeline.
- [[legal-text-classification-sulea-2017]] — a sibling paper applying SVM-based classification to legal text, useful for comparing feature-engineering approaches across legal NLP tasks.

## Future Work

The authors flag three open directions: deeper exploitation of legal-text-specific structure, such as references between articles and structured conditional clauses; broader evaluation of Ranking SVM against other learning-to-rank methods on the same feature set; and further work on the legal question answering component, given that deep learning models did not outperform rule- and feature-based systems on the small COLIEE dataset.

## References

- Kim, Mi-Young, Ying Xu, Randy Goebel. "A Convolutional Neural Network in Legal Question Answering." JURISIN, 2015.
- Carvalho, Danilo S., Minh-Tien Nguyen, Chien-Xuan Tran, Minh-Le Nguyen. "Lexical-Morphological Modeling for Legal Text Analysis." JURISIN, 2015.
- Joachims, T. "Training Linear SVMs in Linear Time." KDD, 2006.
- Kim, Yoon. "Convolutional Neural Networks for Sentence Classification." arXiv:1408.5882, 2014.
- Mikolov, Tomas, Kai Chen, Greg Corrado, Jeffrey Dean. "Efficient Estimation of Word Representations in Vector Space." arXiv:1301.3781, 2013.
- Kim, Mi-Young, Randy Goebel, Yoshinobu Kano, Ken Satoh. "COLIEE-2016: Evaluation of the Competition on Legal Information Extraction and Entailment." JURISIN, 2016.
