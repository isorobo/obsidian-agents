---
type: source
status: draft
created: 2026-08-12
title: "Semantic search: Bringing search experiences into the AI era"
authors: []
organisation: "Elastic (Elasticsearch B.V.)"
source_type: docs
venue: "Elastic white paper"
url: TBD
year: 2023
date_published: 2023
anthropic: false
topic:
- topic/retrieval
- topic/architectures
tags: [semantic-search, vector-search, hybrid-search, sparse-encoder, elser, rag]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
af_targets:
- none
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: be6a386bf31a0aef6d052051402a56b80c075a897e037a6a54ebc6063a442889
---

# Semantic search: Bringing search experiences into the AI era

> Full citation: Elastic. "Semantic search: Bringing search experiences into the AI era." White paper, Elasticsearch B.V., 2023. Document reference wp-semanticsearch-2023-1016.

## Summary

This 18-page Elastic white paper sets out two routes to semantic search and compares their fit for different teams. It opens with the failure modes of keyword search: vocabulary mismatch, semantic mismatch, and domain mismatch. It then names two use cases, retrieving relevant text and supplying context to generative AI through retrieval augmented generation. The middle of the paper contrasts approach one, an out-of-the-box sparse encoder, with approach two, a custom-built dense vector model that needs labelled data and domain adaptation. A decision section, a chapter on hybrid search, and a vendor section on Elastic's own products follow. The paper closes with a customer service case study and a Cisco customer story. The intended reader is a search or platform lead who must choose an implementation route under a delivery deadline, rather than a researcher. Elastic wrote and published the paper, so every performance and product claim carries the vendor's own framing.

## Key Concepts

- Keyword search fails in three ways: vocabulary mismatch, semantic mismatch, and domain mismatch.
- Semantic search applies machine learning to capture the meaning and context of queries and documents.
- Two use cases dominate: retrieving relevant text, and supplying nuanced context to a large language model.
- Retrieval augmented generation feeds proprietary enterprise data to an LLM, which limits cost by passing only relevant data.
- Approach one uses a sparse encoder that works without domain adaptation. It suits beginners, text data, and short timelines.
- Approach two uses dense text embeddings. It suits teams with data science skills, labelled data, multimodal data, and time to iterate.
- Sparse representations hold few non-zero values and score words against documents, rather than encoding meaning in an embedding.
- Hybrid search combines lexical and vector ranking, and improves relevance across the ranking methods combined.
- Elastic reports that Cisco support engineers cut search query response time by 73%, and that a Cisco architect credits Topic Search with resolving 90% of service requests.

## Terminology

- **Lexical search**: traditional retrieval that matches content on keywords.
- **Sparse encoder**: a model that returns relevance scores for words and documents instead of a dense embedding.
- **Term expansion**: the process by which a sparse encoder adds terms to a document based on their relevance to it.
- **Late interaction**: the deferred comparison of query relevance scores against document relevance scores.
- **Dense vector embedding**: a high-dimensional numeric representation where similarity in meaning becomes nearest-neighbour distance.
- **Domain adaptation**: retraining an off-the-shelf embedding model on labelled in-domain data.
- **ELSER**: Elastic Learned Sparse Encoder, Elastic's own retrieval model, licensed commercially within the Elasticsearch Relevance Engine.
- **SPLADE**: the model that introduced the sparse encoder approach. Version two carries no commercial licence.
- **E5**: a family of embedding models from Microsoft researchers that generalise across domains.
- **BM25**: a term-based ranking model used as the lexical baseline throughout the paper.
- **NDCG**: the relevance measure used in the paper, scored between 0 and 1, where higher is better.
- **BEIR**: the heterogeneous zero-shot information retrieval benchmark used for the reported scores.
- **Reciprocal rank fusion (RRF)**: a rank combination method that needs no parameter tuning and no score normalisation.
- **Linear combination**: rank combination as a weighted sum of normalised scores from each ranking.
- **HNSW**: the approximate nearest neighbour algorithm behind Elastic's vector search, implemented in Lucene.

## Architecture and Implementation

The paper splits implementation into a sparse path and a dense path, then adds hybrid ranking on top of either.

On embeddings, the dense path centres on a model trained over large amounts of text. The model runs over knowledge base documents and over query text. Search returns the nearest neighbours among all documents. The paper states that this path assumes the embedding model matches your domain. Without that match, results fall below the lexical baseline. Elastic's reported BEIR averages show ANCE at 0.380 and TAS-B at 0.404 against BM25 at 0.416. The workflow the paper specifies runs in four stages: curate annotated data, evaluate available off-the-shelf models, perform domain adaptation and generate embeddings, then iterate until the deployed application meets its performance criteria. Adaptation may add or replace layers in the neural network. The paper puts fine tuning at weeks to months, and names GPU hardware as a requirement.

On the sparse path, the encoder scores words against documents and expands terms by relevance. A large static vocabulary covering tokens, words, and sub-word units drives generalisation, alongside late interaction between query and document scores. The engineering consequence is direct: sparse vectors sit in the same inverted indices as keyword search, so the same retrieval algorithms apply and no nearest neighbour tuning is needed. Elastic reports out-of-the-box relevance scores of 0.53 for ELSER, 0.49 for E5-base, and 0.48 for SPLADE, against 0.41 for BM25.

On vector search infrastructure, the paper points to approximate nearest neighbour search with HNSW, implemented in Lucene, as the underlying vector database. It argues that a general search platform also supplies aggregations, filtering, faceted search, and auto-complete, which the paper says many dedicated vector databases cover only in part.

On hybrid retrieval and ranking, the paper treats rank combination as the first relevance improvement to try, whichever semantic model is in place. Lexical and semantic ranking complement each other. Keyword search handles single-word queries, exact brand matches, and domain-specific terminology. Embedding models handle multi-word queries, concept searches, and questions. RRF requires no tuning and no score normalisation. Linear combination weights each ranking, stays interpretable, and needs normalised scores plus annotations similar to fine-tuning data. Optimal weights shift between datasets. Elastic reports NDCG@10 averages over a BEIR subset of 0.439 for BM25, 0.512 for ELSER, 0.519 for hybrid RRF, and 0.543 for a tuned linear combination. The paper frames these as gains of about 1% for RRF and 5% for an optimised linear combination.

The deployment recipe for the Elastic out-of-the-box path runs in three steps. Download the model to dedicated machine learning nodes in the cluster. Apply the model to data at ingest or as a post-processing step. Execute queries through the same `_search` endpoint used for BM25 search.

## Code Examples

The paper carries no code. The single concrete API detail is the reuse of the `_search` endpoint for semantic queries, which the paper cites as evidence that no separate query path is required.

## Best Practices

- Choose the approach against four factors: AI experience, data types, time horizon, and availability of labelled data.
- Pick the out-of-the-box sparse model when the timeline is short and the data is text.
- Pick the dense vector approach when the use case needs tuning, non-textual data, or your own embeddings.
- Try hybrid search first when improving relevance, whichever semantic model is in place.
- Use RRF where no tuning budget exists, since it needs no parameter tuning and no score normalisation.
- Reserve linear combination for teams that hold data analytics expertise.
- Curate documents and queries with known relevance rankings before evaluating retrieval performance.
- Budget weeks to months for fine tuning an embedding model, and acquire GPU hardware to hold training time down.
- Monitor performance after deployment and ingest new data as it arrives.
- Treat the progression as staged: out-of-the-box model, then hybrid search, then dense vector search, then generative AI on top.

## Warnings and Anti-Patterns

- Configuring keyword search alone leaves vocabulary, semantic, and domain mismatch unresolved.
- Deploying a public embedding model without domain adaptation risks scoring below the BM25 baseline, as the paper's BEIR table shows for ANCE and TAS-B.
- Adopting SPLADE version two for a commercial product fails on licensing. The paper states it carries no commercial licence.
- Expecting to tune the sparse approach beyond hybrid search will disappoint. The paper lists tuning as its weakness.
- Sending non-text data down the sparse path fails. Sparse encoders handle text only.
- Bringing your own embeddings rules the sparse path out.
- Reading dense vector scores for explanation fails, since embedding representations resist interpretation.
- Calibrating a linear combination without normalised scores and annotations produces unreliable weights, and optimal weights vary between datasets.
- Dense vector search draws heavily on compute and storage.
- Read every relevance number, product comparison, and Fortune 500 adoption claim in the paper as Elastic's own measurement and marketing.

## Related Concepts

- [[evaluation]]
- [[memory]]
- [[retrieval-augmented-generation]] - covers hybrid search, rank fusion, and reranking
- [[knowledge-graph]]
- [[graphrag]]

## Future Work

The paper flags the space as fast-moving and names further optimisation as open. It sets out a staged progression from an out-of-the-box model, through hybrid search, to dense vector search, then generative AI on top. It cites a Google survey reporting that executives feel urgency to adopt generative AI while judging the technology unready for production, and positions semantic search as the production-ready part of that gap. It defers the mechanics of domain adaptation, data ingestion, and query construction to external Elastic guides and an interactive demo, none of which the extract resolves to a URL.

## References

- Elastic. "Semantic search: Bringing search experiences into the AI era." White paper, Elasticsearch B.V., 2023. Document reference wp-semanticsearch-2023-1016. Publisher site stated in the document footer: elastic.co. Canonical URL not stated in the extract.
- Google survey on what business leaders expect from generative AI, published 26 May 2023.
- Grebennikov, R. "From zero to semantic search embedding model." 12 June 2023.
- Wang, L. et al. "Text Embeddings by Weakly-supervised Contrastive Pre-training." December 2022.
- Thakur, N. et al. "BEIR: A Heterogeneous Benchmark for Zero-shot Evaluation of Information Retrieval Models." UKP Lab, Technical University of Darmstadt, 2021.
