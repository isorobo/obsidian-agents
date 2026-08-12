---
type: moc
status: draft
created: 2026-08-12
name: Retrieval
topic:
- topic/retrieval
tags: []
wiki_role: moc
---

# MOC - Retrieval

> Retrieval systems that ground an agent: vector search, knowledge graphs, and GraphRAG.

## Start Here

The first notes to read in this topic. Read the three concepts before the sources.

1. [[retrieval-augmented-generation]]
2. [[knowledge-graph]]
3. [[graphrag]]

## Core Notes

Curated wikilinks, grouped by sub-theme.

### Concepts

- [[retrieval-augmented-generation]] - retriever plus generator, chunking, hybrid search
- [[knowledge-graph]] - property graph model, entity resolution, ontologies
- [[graphrag]] - graph traversal joined to vector retrieval for multi-hop questions

### Knowledge graph foundations

- [[10_Sources/Docs/graph-databases-for-rdbms-developers-neo4j-2021|Graph Databases for the RDBMS Developer]]
- [[10_Sources/Docs/how-to-build-a-knowledge-graph-neo4j-2025|How to Build a Knowledge Graph]]

### GraphRAG

- [[10_Sources/Books/essential-graphrag-bratanic-2025|Essential GraphRAG]]
- [[10_Sources/Docs/semantic-advantage-graphrag-graphwise-2026|The Semantic Advantage]]

### Vector and hybrid search

- [[10_Sources/Docs/semantic-search-ai-era-elastic-2023|Semantic Search in the AI Era]]

## All Notes in This Topic

```dataview
LIST
FROM ""
WHERE contains(topic, "topic/retrieval") AND type != "moc"
SORT file.name ASC
```

## Related Maps

- [[MOC - Home]]
- [[MOC - Memory]]
- [[MOC - Architectures]]
