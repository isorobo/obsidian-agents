---
type: source
status: draft
created: 2026-08-12
title: "Essential GraphRAG: Knowledge Graph-Enhanced RAG"
authors:
- Tomaž Bratanič
- Oskar Hane
organisation: "Manning Publications"
source_type: book
venue: "Manning Publications, Shelter Island"
url: https://www.manning.com/books/essential-graphrag
year: 2025
date_published: 2025
anthropic: false
topic:
- topic/retrieval
- topic/architectures
tags: [graphrag, knowledge-graphs, neo4j, cypher, agentic-rag, rag-evaluation]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
---

# Essential GraphRAG: Knowledge Graph-Enhanced RAG

> Full citation: Bratanič, T. and Hane, O. "Essential GraphRAG: Knowledge Graph-Enhanced RAG." Manning Publications, Shelter Island, 2025. ISBN 9781633434394. Foreword by Paco Nathan. https://www.manning.com/books/essential-graphrag

## Summary

Essential GraphRAG shows how to build retrieval-augmented generation on top of a knowledge graph. Bratanič and Hane both work at Neo4j, and every chapter runs against a Neo4j instance. The book opens on the limits of large language models: knowledge cutoff, outdated facts, hallucination, and no access to private data. It rejects continuous finetuning as the fix and argues for RAG. It then argues that a knowledge graph holds structured and unstructured data in one store, so one system answers both fuzzy and precise questions. Eight chapters progress from vector similarity search and hybrid search to advanced retrieval strategies. Later chapters cover text2cypher, agentic RAG, graph construction with LLMs, Microsoft's GraphRAG, and evaluation. An appendix documents the Neo4j environment, the Cypher query language, the APOC plugin, and the Graph Data Science library. The authors build each system from scratch rather than through a framework such as LangChain. Worked datasets include an arXiv paper on Einstein's patents, the CUAD legal contract corpus, The Odyssey, and a movies graph. Code sits in Jupyter notebooks, one per chapter, in the companion repository at github.com/tomasonjo/kg-rag. The book targets data scientists, software engineers, and developers who know Python and the basics of LLMs.

## Key Concepts

- RAG grounds an LLM in an external knowledge base, cutting hallucination and knowledge-cutoff error.
- Supervised finetuning fails as a route to fresh facts; research shows LLMs struggle to learn new facts this way.
- A knowledge graph stores structured and unstructured data in one database, with nodes as entities and relationships as connections.
- Text embeddings retrieve semantic similarity. They fail at filtering, sorting, counting, and aggregation, which need structured data.
- A RAG architecture splits into two components: a retriever and a generator.
- Hybrid search joins vector similarity with a full-text index to combine precise term matching and broad meaning.
- Step-back prompting rewrites a narrow question into a broader one before vector search.
- Parent document retrieval embeds small child chunks, then returns the whole parent document as context.
- Text2cypher converts a natural language question into a Cypher query over the graph.
- Agentic RAG rests on three parts: a retriever router, retriever agents, and an answer critic.
- Microsoft's GraphRAG extracts entities and relationships, detects communities, and summarises each community with an LLM.
- Global search runs a map-reduce over community summaries. Local search starts from entities found by vector search.
- Evaluation rests on three metrics from RAGAS: context recall, faithfulness, and answer correctness.

## Terminology

- **Knowledge graph**: a data structure that uses nodes for entities and concepts, and relationships to connect them.
- **Retriever**: the RAG component that finds relevant information and passes it to the generator.
- **Generator**: the LLM that writes the answer from the retrieved context.
- **Hybrid search**: retrieval that merges vector similarity search with full-text keyword search.
- **Step-back prompting**: a query-rewriting technique that broadens a specific question to raise retrieval recall.
- **Parent document retriever**: a strategy that embeds child chunks and returns the parent document.
- **Text2cypher**: generation of a Cypher query from a natural language question.
- **Retriever router**: a function, usually an LLM, that picks the best retriever or retrievers for a question.
- **Answer critic**: a blocking function that checks whether the retrieved answer resolves the original question.
- **Entity resolution**: merging different representations of the same real-world entity within a graph.
- **Community**: a group of entities more densely connected to each other than to the rest of the graph.
- **Global search**: retrieval that aggregates community summaries through a map step and a reduce step.
- **Local search**: retrieval that starts from entities matched by vector search, then pulls connected nodes, relationships, chunks, and community summaries.
- **Context recall**: the share of relevant information the retrieval system captured.
- **Faithfulness**: whether every claim in the answer follows from the retrieved context.
- **Answer correctness**: how accurately and completely the response addresses the query.

## Architecture and Implementation

The book specifies a layered build on Neo4j. Chapter 2 sets the base: chunk the text, embed each chunk with an embedding model, write the vectors to Neo4j, and create a vector index. A full-text index sits beside the vector index so the retriever runs hybrid search. The generator then receives the retrieved chunks inside a prompt template alongside the user question.

Chapter 3 raises retrieval accuracy through two changes. An LLM rewrites the user question into a broader step-back question, guided by a system prompt with few-shot examples. The document is split by structural headings, then into parent documents of at most 2,000 characters, then into 500-character child documents. The graph stores a PDF node, HAS_PARENT relationships to parent nodes, and HAS_CHILD relationships to child nodes. The embedding sits on the child node; retrieval matches the child and returns the parent text.

Chapter 4 specifies the text2cypher retriever. The prompt carries four parts: few-shot question and Cypher pairs, the graph schema with labels, relationship types, and properties, terminology mappings from user vocabulary to schema names, and format instructions. Neo4j publishes an open training dataset and finetuned models on Hugging Face for teams that need a smaller, faster generator.

Chapter 5 specifies agentic RAG through OpenAI function calling, with ReAct named as the alternative for models without tool support. Each retriever is a Python function paired with a JSON tool description. The worked set holds two Cypher template retrievers, movie by title and movies by actor, plus text2cypher as the fallback. The router picks a tool and extracts its arguments. The answer critic then inspects the retrieved context and either releases the answer or issues a new question for another round. The loop needs an exit condition for data the graph does not hold.

Chapter 6 specifies graph construction from text. A Pydantic model defines the target schema, and the OpenAI Structured Outputs feature forces the extraction to match it. The contract model holds Contract, Organization, and Location nodes, with HAS_PARTY and LOCATED_AT relationships. Unique constraints on Contract.id, Organization.name, and Location.fullAddress protect integrity and query speed. A MERGE-based Cypher statement imports the extracted dictionary. Entity resolution then merges name variants such as "Limited" and "Ltd". The schema later gains Chunk nodes so the original unstructured text sits beside the extracted structure.

Chapter 7 reimplements Microsoft's GraphRAG pipeline over The Odyssey. Indexing runs in two stages. Stage one chunks the text along the 24 books, extracts entities and relationships with an LLM, and summarises each entity and relationship across chunks. Stage two runs the Louvain algorithm from the Graph Data Science library to detect communities, then generates a structured report per community. The report prompt fixes the output shape: title, summary, impact severity rating, rating explanation, and five to 10 detailed findings. Retrieval then runs global search or local search. Global search maps each community report to key points with importance ratings, then reduces the top points into one answer. Local search embeds entity summaries into a vector index, finds entry-point entities, and ranks connected chunks, relationships, entities, and community summaries into a bounded context window.

Chapter 8 specifies evaluation with the RAGAS library over a 17-example benchmark. Ground truth is a Cypher query rather than a fixed string, so the benchmark survives data change. The reported run scored 0.7774 on answer correctness, 0.7941 on context recall, and 0.9657 on faithfulness.

## Code Examples

The companion repository at https://github.com/tomasonjo/kg-rag holds one Jupyter notebook per chapter, from ch02.ipynb to ch08.ipynb, plus Python scripts and environment setup instructions. Reusable listings include the step-back system prompt with few-shot examples, the section-splitting regular expression, a `num_tokens_from_string` helper built on tiktoken, the OpenAI tool-description dictionaries for each retriever, the Pydantic contract schema for Structured Outputs, the MERGE-based contract import statement, the unique constraint definitions, the Louvain community call, the community summarisation prompt, and the entity embedding and vector index creation for local search. Executable snippets also ship through Manning liveBook.

## Best Practices

- Split text on structural elements such as sections and paragraphs before splitting on character count.
- Count tokens per chunk before import. Split anything past a safe limit and drop chunks of 20 tokens or fewer.
- Embed child chunks for precision and return the parent document for context.
- Add few-shot examples to the text2cypher prompt for each mistake pattern you observe.
- Put the graph schema in the prompt and forbid labels, relationship types, and properties outside it.
- Add terminology mappings so user vocabulary lands on the right schema element.
- Build narrow, specialised retrievers over time for questions the generic retrievers handle badly.
- Keep text2cypher as the catch-all retriever behind the specialised ones.
- Define unique constraints and indexes on every node key before import.
- Define entity resolution rules from domain ontologies, with subject matter experts setting the matching criteria.
- Store the original unstructured document alongside the extracted structure in the same graph.
- Chunk domain documents on their semantic units, such as contract clauses, rather than on token count alone.
- Choose entity types before extraction, since they shape extraction, linking, and summarisation quality.
- Write benchmark ground truth as a Cypher query so the dataset stays valid as data changes.
- Cover greetings, scope questions, irrelevant questions, and missing-data cases in the benchmark.
- Grow the benchmark as the system grows.

## Warnings and Anti-Patterns

- Continuous finetuning to refresh factual knowledge remains costly and unreliable in production.
- Chunking across many documents returns top-k chunks from the wrong document. A payment-terms question pulls terms from unrelated contracts.
- Relying on embeddings alone breaks any question that needs filtering, sorting, counting, or aggregation.
- Embedding a whole long document blurs distinct ideas through averaging and weakens matching.
- The contract import statement in listing 6.13 uses `randomUUID()` and is not idempotent. Repeat runs create duplicate contracts.
- Skipping entity resolution leaves several nodes for one real-world entity and corrupts counts and traversals.
- A single generic entity resolution rule fails across domains. Financial thresholds misfire on biomedical entities.
- Louvain is not deterministic. Communities shift between runs on the same graph.
- Low community levels give detail at the cost of more LLM calls and latency. High levels lose granularity.
- Text2cypher adds an LLM call, and the book measures higher latency on every query that uses it.
- An LLM judge scores inconsistently on trivial cases such as a greeting.
- The agent failed the question "Who has the longest name among all actors?" because it could not write the Cypher. Cover such gaps with a few-shot example or a dedicated tool.
- Finetuning an embedding model forces a recompute of every stored embedding.

## Related Concepts

- [[tool-use]]
- [[react]]
- [[evaluation]]
- [[the-agent-loop]]
- [[retrieval-augmented-generation]]
- [[knowledge-graph]]

## Future Work

Section 8.3 flags the direction rather than a research gap. The authors expect LLMs to improve at tool use for retrieval, transformation, and manipulation, so complex tasks need less prompting. System quality then rests on the design and integration of the tools the builder supplies. The book leaves graph data modelling out of scope and points readers to Neo4j GraphAcademy. It also leaves most advanced retrieval techniques unimplemented: embedding model finetuning, reranking, metadata filtering, and hypothetical question embedding all get a description without code. Chapter 7 skips the hierarchical community structure of the Louvain algorithm that the Microsoft paper uses, since the worked graph is small.

## References

- Bratanič, T. and Hane, O. "Essential GraphRAG: Knowledge Graph-Enhanced RAG." Manning Publications, 2025. ISBN 9781633434394. https://www.manning.com/books/essential-graphrag
- Companion code repository: https://github.com/tomasonjo/kg-rag
- liveBook edition: https://livebook.manning.com/book/essential-graphrag
- Edge et al., 2024. Microsoft GraphRAG. https://github.com/microsoft/graphrag
- Lewis et al., 2020. Retrieval-augmented generation.
- Zheng et al., 2023. Step-back prompting.
- Vaswani et al., 2017. Transformer architecture.
- Neo4j text2cypher training dataset: https://huggingface.co/datasets/neo4j/text2cypher
- Neo4j finetuned text2cypher models: https://huggingface.co/neo4j
