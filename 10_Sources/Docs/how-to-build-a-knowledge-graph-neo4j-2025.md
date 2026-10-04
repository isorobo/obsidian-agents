---
type: source
status: draft
created: 2026-08-12
title: "The Developer's Guide: How to Build a Knowledge Graph"
authors: []
organisation: "Neo4j"
source_type: docs
venue: "Neo4j ebook"
url: TBD
year: 2025
date_published: 2025-07-11
anthropic: false
topic:
- topic/retrieval
- topic/architectures
tags: [knowledge-graph, graph-database, cypher, graphrag, entity-resolution, data-modelling]
nlm_id: 
nlm_skip: false
watchlist_channel: 
authored_by: agens
af_targets:
- none
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: c3bc8f9e0593fbc3bec6e43fe732597e627dc0d1eaefeb94df8ebff71cb75ba6
---

# The Developer's Guide: How to Build a Knowledge Graph

> Full citation: Neo4j. "The Developer's Guide: How to Build a Knowledge Graph." Neo4j ebook, 2025.

## Summary

This Neo4j ebook teaches a developer to build a first knowledge graph end to end on the hosted AuraDB graph database. It opens with the failures of relational systems: information silos, costly join operations, and fixed schemas that resist change. It then defines a knowledge graph as entities and relationships in one interconnected structure, and names three components: nodes, relationships, and organising principles. The practical core walks through account signup, instance creation, model design in Data Importer, CSV loading from the Northwind retail dataset, and querying with Cypher. Three Cypher clauses carry the query section: MATCH, CREATE, and MERGE. The final third covers expansion routes, including unstructured data loaded through the LLM Knowledge Graph Builder, graph algorithms, and three use cases: supply chain, entity resolution, and GenAI. The reader is a developer with relational database experience and no graph background. Jennifer Reif, John Stegeman, and Damaso Sanoja contributed technical review.

## Key Concepts

- A knowledge graph maps entities, which are objects, events, or concepts, and their relationships into one interconnected structure.
- Three components make up any knowledge graph: nodes, relationships, and organising principles.
- Organising principles bring business context by defining hierarchies and categories over entities, relationships, and properties.
- In a property graph database, the conceptual data model and the physical data model are the same artefact.
- A flexible schema admits new entity types and relationship types without disruptive migration.
- Knowledge graphs integrate structured and unstructured data in one store, which supports GraphRAG.
- Graph structure exposes patterns that relational tables hide, such as supplier concentration in one hurricane-prone region.
- Graph algorithms extend the graph beyond stored data: node similarity for recommendation, pathfinding for supply chain routes.

## Terminology

- **Node** - an instance of an entity, such as a person, a place, a concept, or an event.
- **Relationship** - a directed connection that records how two nodes interact, such as `DIAGNOSED_WITH` or `PURCHASED`.
- **Property** - an attribute on a node or a relationship, such as `unitPrice` on a product or `quantity` on an order line.
- **Label** - a classifier that identifies a node by role or type, such as `Patient` or `Product`.
- **Organising principle** - the structure that defines node types, relationship types, hierarchies, and categories for the domain.
- **Cypher** - the declarative graph query language, the widest adopted implementation of the ISO GQL standard.
- **MATCH** - the Cypher clause that finds nodes or patterns, comparable to `SELECT` in SQL.
- **CREATE** - the Cypher clause that adds new data, comparable to `INSERT` in SQL.
- **MERGE** - the Cypher find-or-create clause: it returns an existing pattern or creates a missing one.
- **GraphRAG** - graph-based retrieval-augmented generation, which grounds an LLM in knowledge graph data.
- **Entity resolution** - the process of deciding whether several records reference the same real-world entity.

## Architecture and Implementation

The guide builds on Neo4j AuraDB, a cloud-hosted managed graph database. The reader signs up through the Aura Console, then creates an instance. The Free tier serves learning; the Professional tier serves production workloads. Aura issues a credentials file at instance creation, and the password stays unavailable after that download.

Data modelling comes before data. The reader opens Data Importer from the Aura console and clicks Define Manually to sketch the model. The worked example is a simplified Northwind retail graph. It carries five node types and four relationship types. `Customer` holds `customerID`, `companyName`, and `city`. `Order` holds `orderID`, `orderDate`, and `shippedDate`. `Product` holds `productID`, `productName`, and `unitPrice`. `Supplier` holds `supplierID`, `companyName`, and `city`. `Category` holds `categoryID` and `categoryName`. The relationships are `PURCHASED` from customer to order, `ORDERS` from order to product, `SUPPLIES` from supplier to product, and `PART_OF` from product to category. Relationships carry properties too: `ORDERS` holds `quantity`. Direction matters. The guide contrasts `Customer-PURCHASED->Order` with a `Customer-CREATES->Order` pattern that would model an unpurchased cart. The model gains its organising principle from the product hierarchy expressed by `Category` and `PART_OF`.

Ingestion follows the model. The reader downloads six CSV files from the Northwind GitHub repository: `categories.csv`, `customers.csv`, `order-details.csv`, `orders.csv`, `products.csv`, and `suppliers.csv`. Drag and drop loads them into the Data sources pane. Each node and each relationship maps to one file through the Table field on the Definition tab. Relationships need a further step: Node ID mapping supplies the From and To keys. Where model property names match CSV column names, the Map from table button fills the mapping in one action. A green checkmark marks each fully mapped element. Run import loads the data and reports the outcome. The importer also connects to PostgreSQL, MySQL, and SQL Server, so structured data can move from a relational source without an intermediate file.

Querying uses Cypher, a declarative language that states the wanted result rather than the access path. Its pattern syntax mirrors a whiteboard drawing: `(c:Customer)-[r:ORDERS]->(p:Product)`. `MATCH` retrieves patterns, and inline maps filter them, as in `(c:Category {categoryName: "Beverages"})`. Aggregation, collection, and ordering work inside a `RETURN`, which lets one query name the customers affected by a stock-out, count their orders, and list the order IDs. A single query traverses customer, order, product, category, and supplier in one pattern, which answers a multistep question without joins. `CREATE` always writes new data. `MERGE` runs find-or-create over a whole pattern.

Entity resolution appears as a use case rather than a build step. Hand-written comparison queries cost development effort and run time. A knowledge graph reduces both. Shared identifiers and attributes model as separate nodes, which exposes candidates for merging. Weakly connected components segments the graph into communities, and nodes in separate communities need no comparison, which cuts the comparison count. The graph also speeds transitive comparisons, needed where more than two digital records represent one real-world entity.

Unstructured data extends the same graph. The LLM Knowledge Graph Builder extracts nodes and relationships from documents such as PDF invoices, and stores vector representations beside the structured data. Integration with an existing graph takes two steps. First, set the merge key with `MATCH (p:Product) SET p.id=p.productName, p:__Entity__`. Second, open Graph Enhancement, choose Load Existing Schema, and verify the suggested labels and relationship types. The Builder then attaches extracted invoice data to existing product nodes instead of creating duplicates.

## Code Examples

The guide carries four reusable Cypher snippets. The first finds every product in one category and returns the nodes and relationships for visualisation:

```cypher
MATCH (p:Product)-[rel:PART_OF]->(c:Category {categoryName: "Beverages"})
RETURN p, rel, c;
```

The second answers a stock-out question. It returns the affected customers, their order counts, and the order IDs, sorted by impact:

```cypher
MATCH (c:Customer)-[r1:PURCHASED]->(o:Order)-[r2:ORDERS]->(p:Product {productName: "Ipoh Coffee"})
RETURN c.companyName, COUNT(o) AS orders, collect(o.orderID)
ORDER BY orders DESC;
```

The third traverses five node types in one pattern to link a category to its customers and its suppliers:

```cypher
MATCH (cust:Customer)-[r1:PURCHASED]->(o:Order)-[r2:ORDERS]->(p:Product)-[r3:PART_OF]->(c:Category {categoryName:"Produce"}),
      (p)<-[r4:SUPPLIES]-(s:Supplier)
RETURN *;
```

The fourth shows idempotent writes. Separate `MERGE` statements per node and per relationship allow repeated runs without duplicates:

```cypher
MERGE (p:Product {productID: 78, productName: "Organic Quinoa"})
MERGE (c:Category {categoryID: 9, categoryName: "Grains/Cereals"})
MERGE (p)-[r:PART_OF]->(c)
RETURN *;
```

## Best Practices

- Design the model before loading data. Draw nodes, relationships, and properties in Data Importer first.
- Give the model an organising principle. A product hierarchy or an order fulfilment process supplies one.
- Name model properties to match the source column names. Map from table then fills the mapping in one step.
- Set relationship direction to state the business meaning. `PURCHASED` and `CREATES` describe different states of an order.
- Put properties on relationships where the fact belongs to the connection, such as `quantity` on `ORDERS`.
- Split a `MERGE` into one statement per node and one per relationship to keep writes idempotent.
- Save the credentials file at instance creation. The password stays unavailable afterwards.
- Set the `__Entity__` label and an `id` property before running the LLM Knowledge Graph Builder against an existing graph.
- Load an existing schema into the Builder so extracted labels and relationship types match the graph.

## Warnings and Anti-Patterns

- Merging a whole pattern in one statement creates duplicate nodes when the nodes exist and the relationship does not.
- Cypher matches complete patterns, not single elements. A partial match creates the entire pattern anew.
- `CREATE` writes new data even where identical data exists. Use `MERGE` where duplication would corrupt the graph.
- Releasing the drag before reaching the target node creates a blank node instead of a relationship.
- Relational storage of connected data loses the context around it, and reconstructing that context through joins degrades runtime.
- A fixed relational schema resists change, which erodes the business value of the store over time.
- An LLM answers without real-time data, without private data, and without a cited source, which yields outdated or wrong output.
- A supply chain with one supplier per product carries no backup. The guide surfaces this risk through a graph query.

## Related Concepts

- [[knowledge-graph]] - covers entity resolution, the property graph model, and ontologies
- [[graphrag]]
- [[cypher-query-language]]
- [[graph-database]]
- [[memory]]

## Future Work

The guide names three expansion routes and leaves each to the reader. First, widen the data scope: add customer attributes such as location, industry, or revenue as further organising principles, add clickstream behaviour to support recommendation, and add supply chain data to model disruption risk. Second, load unstructured sources through the LLM Knowledge Graph Builder and apply GraphRAG over the combined graph. Third, run graph algorithms such as node similarity and pathfinding to surface patterns the stored data leaves implicit. The guide points to GraphAcademy courses, the Neo4j Community, an article series on graph data science for supply chains, and companion pieces on entity resolution and GraphRAG.

## References

- Neo4j. "The Developer's Guide: How to Build a Knowledge Graph." Neo4j ebook, 2025. Local copy: `10_Sources/PDFs/developers-guide-how-to-build-knowledge-graph.pdf`. Canonical URL: TBD.
- Cited within the guide: Neo4j GraphAcademy, Cypher Fundamentals course; Neo4j LLM Knowledge Graph Builder; "Graph Data Science Use Cases: Entity Resolution"; "What Is GraphRAG"; the Northwind GitHub CSV dataset.
