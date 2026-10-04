---
type: concept
status: draft
created: 2026-08-12
name: Cypher Query Language
slug: cypher-query-language
topic:
- topic/retrieval
- topic/concepts
tags: [cypher, graph-query-language, neo4j, property-graph, text2cypher]
synonyms: [Cypher, openCypher, GQL]
defined_in: "[[10_Sources/Docs/graph-databases-for-rdbms-developers-neo4j-2021|Graph Databases for the RDBMS Developer]]"
related_concepts: ["[[graph-database]]", "[[knowledge-graph]]", "[[graphrag]]", "[[tool-use]]", "[[index-free-adjacency]]", "[[polyglot-persistence]]"]
authored_by: agens
af_targets:
- none
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: ad25f4b33a1fd0a609333ae7428d5ab3b9321bdec199fdf4e8185de273aa407b
---

# Cypher Query Language

> Cypher is the declarative query language for property graphs, and it draws the wanted pattern in ASCII art rather than naming the access path.

## Summary

Cypher states the result a caller wants, not the route the engine takes. Neo4j
sponsored the language, and the openCypher project widened it beyond one vendor. The 2025
Neo4j guide names Cypher the widest adopted implementation of the ISO GQL standard. Its
pattern syntax mirrors the diagram a team draws on a whiteboard, so the query and the model
share one shape. For an RDBMS developer, the payoff arrives in the comparison: a traversal
that reads in two lines replaces a chain of JOINs. For an agent, Cypher is the interface to
a [[graph-database]], and text-to-Cypher makes that interface a tool.

## Key Concepts

- Parentheses draw nodes, paired dashes draw relationships, and angle brackets set direction.
- A colon prefixes a label or a relationship type; curly braces hold property key-value pairs.
- `MATCH` finds patterns and fills the role `SELECT` fills in SQL.
- `WHERE` filters matches, and `RETURN` names what goes back to the client.
- `CREATE` writes new data even where identical data exists.
- `MERGE` runs find-or-create over a whole pattern.
- Cypher operates on complete patterns, not single elements.
- One arrow in a `MATCH` maps to a many-to-many JOIN table with two JOINs.
- Text-to-Cypher lets a model query a graph, and it fails on an invalid query or an unseen schema.

## Detail

### Pattern syntax

A node sits inside parentheses, as in `(a:Person {name:'Jim'})`. A relationship sits between
paired dashes, with the type in square brackets after a colon, as in `-[:KNOWS]->`. The `<`
and `>` signs carry direction. A triangle of three mutual friends reads as one line:
`(emil)<-[:KNOWS]-(jim)-[:KNOWS]->(ian)-[:KNOWS]->(emil)`. A pattern alone binds to no data.
The writer anchors part of it with a label and a property value. Cypher then matches the
remainder of the pattern around that anchor point.

```cypher
MATCH (a:Person {name:'Jim'})-[:KNOWS]->(b:Person)-[:KNOWS]->(c:Person), (a)-[:KNOWS]->(c)
RETURN b, c
```

That query returns the mutual friends of Jim. The identifier `a` stays bound to Jim. The
identifiers `b` and `c` bind to a sequence of nodes as the query runs.

### Core clauses

`MATCH` sits at the heart of most Cypher queries. `WHERE` supplies criteria that filter the
matched patterns. `RETURN` specifies the expressions, relationships, and properties sent to
the client. `CREATE` and `CREATE UNIQUE` write nodes and relationships. `MERGE` ensures the
supplied pattern exists, either by reusing matching elements or by creating new ones.
`DELETE` and `REMOVE` strip nodes, relationships, and properties. `SET` writes property
values and labels. `ORDER BY`, `SKIP LIMIT`, `FOREACH`, and `UNION` follow the SQL habits an
RDBMS developer holds. `WITH` chains query parts and forwards results from one to the next,
which the 2021 guide compares to piping commands in Unix.

Aggregation, collection, and ordering all sit inside a `RETURN`. One query names the
customers hit by a stock-out, counts their orders, and lists the order IDs:

```cypher
MATCH (c:Customer)-[r1:PURCHASED]->(o:Order)-[r2:ORDERS]->(p:Product {productName: "Ipoh Coffee"})
RETURN c.companyName, COUNT(o) AS orders, collect(o.orderID)
ORDER BY orders DESC;
```

### The traversal against the join

One question, two languages. List the employees in the IT Department. SQL walks a JOIN table:

```sql
SELECT name FROM Person
LEFT JOIN Person_Department ON Person.Id = Person_Department.PersonId
LEFT JOIN Department ON Department.Id = Person_Department.DepartmentId
WHERE Department.name = "IT Department"
```

Cypher states the pattern:

```cypher
MATCH (p:Person)<-[:EMPLOYEE]-(d:Department)
WHERE d.name = "IT Department"
RETURN p.name
```

Neo4j measures the Cypher at half the length of the SQL. The join names two key columns per
table pair. The traversal names the relationship type once.

A second pair widens the gap. This query builds a co-purchase recommendation:

```cypher
MATCH (u:Customer {customer_id:'customer-one'})-[:BOUGHT]->(p:Product)
      <-[:BOUGHT]-(peer:Customer)-[:BOUGHT]->(reco:Product)
WHERE not (u)-[:BOUGHT]->(reco)
RETURN reco as Recommendation, count(*) as Frequency
ORDER BY Frequency DESC LIMIT 5;
```

Each arrow in that `MATCH` maps to a many-to-many JOIN table with two JOINs, so three arrows
cover six JOINs. The SQL equivalent nests a three-way self-join over
`Customer_product_mapping` inside a subquery, adds a `not in` subquery for products the
customer holds, then groups and orders the outer result. Neo4j measures it at three times the
length of the Cypher.

### Depth

A Cypher pattern grows by one arrow per hop. The SQL equivalent grows by two JOINs per hop.
Hierarchies and trees push SQL into recursive self-JOINs, which the 2021 guide names among
the longest SQL queries in the world. [[index-free-adjacency]] turns each hop into a pointer
hop, so traversal time holds as the dataset grows. Neither Neo4j guide prints the
variable-length quantifier, so this note stops at fixed-length patterns. Each routes deeper
path syntax onward: the 2021 guide to the Cypher Refcard, the 2025 guide to the Cypher
Fundamentals course on GraphAcademy.

### Writing data

`CREATE` always writes new data. `MERGE` combines `MATCH` and `CREATE`: it returns the
existing pattern or saves a missing one. The pattern rule bites on writes. Where a `MERGE`
covers a whole pattern, and the nodes exist while the relationship does not, Cypher creates
the entire pattern and produces duplicate nodes. Split the write into one `MERGE` per node
and one per relationship:

```cypher
MERGE (p:Product {productID: 78, productName: "Organic Quinoa"})
MERGE (c:Category {categoryID: 9, categoryName: "Grains/Cereals"})
MERGE (p)-[r:PART_OF]->(c)
RETURN *;
```

That statement runs many times over without creating duplicates.

### Cypher as an agent tool

Text-to-Cypher converts a natural language question into a query the system executes. It
reaches the questions vector search cannot answer: filtering, sorting, counting, and
aggregation. Bratanič and Hane give the shape with a rating question over a movie graph:

```cypher
MATCH (:Reviewer)-[r:REVIEWED]->(m:Movie)<-[:DIRECTED]-(:Director {name: 'Steven Spielberg'})
RETURN m.title, AVG(r.score) AS avg_rating
ORDER BY avg_rating DESC LIMIT 3
```

Under [[tool-use]], the agent holds text2cypher as one tool beside narrow retrievers, and it
serves as the catchall where no specific retriever fits. Two failure modes govern the design.

The first is an invalid generated query. LLMs make mistakes on complex questions, on
ambiguous questions, and on schema elements without semantic names. The worked agent in
Essential GraphRAG failed "Who has the longest name among all actors?" because the model
could not generate the Cypher. The fixes are a few-shot example or a dedicated tool for that
question shape.

The second is a schema the model has not seen. Without a schema in the prompt, the LLM
assumes the names of nodes, relationships, and properties. A supplied schema maps the
semantics of the question onto the graph model: the labels in use, the relationship types
that exist, the available properties, and which types connect. Neo4j's internal research
finds the format of that schema description carries little weight, so presence matters more
than shape. Schema inference runs through the APOC library, and sampling replaces a full
scan on a large database. Terminology mapping closes the last gap. Where the model reads a
property that the graph holds as a node, a few-shot example corrects the pattern:

```cypher
MATCH (m:Movie {title: 'The Matrix'})-[:PRODUCED_IN]->(c:Country)
RETURN c.name
```

## Trade-offs and Limits

Cypher earns its length advantage on connected data. A tabular workload over one table suits
SQL, which is the case for [[polyglot-persistence]] rather than migration. Length cuts both
ways: a short wrong pattern returns wrong rows with no JOIN to blame. Pattern semantics catch
writers out, and a whole-pattern `MERGE` duplicates nodes where the nodes exist and the
relationship does not. `CREATE` writes a second copy where the data exists, so a repeatable
load needs `MERGE`.

Text2cypher costs one LLM call per query and raises latency on every question it handles.
Few-shot examples bind to one [[knowledge-graph]], so each graph needs its own set, written
by hand. Terminology mappings grow as the failures surface, which makes them maintenance
work rather than setup work. Schema inference over a large database costs enough that Neo4j
recommends sampling. Statements sent over HTTP or JDBC take parameters, which protects
against injection and lets the engine reuse the plan.

## Related

- [[graph-database]]
- [[knowledge-graph]]
- [[graphrag]]
- [[tool-use]]
- [[index-free-adjacency]]
- [[polyglot-persistence]]

## Sources

- [[10_Sources/Docs/graph-databases-for-rdbms-developers-neo4j-2021|Graph Databases for the RDBMS Developer]]
- [[10_Sources/Docs/how-to-build-a-knowledge-graph-neo4j-2025|How to Build a Knowledge Graph (Neo4j)]]
- [[10_Sources/Books/essential-graphrag-bratanic-2025|Essential GraphRAG]]

## See also

- [[MOC - Concepts]]
- [[MOC - Retrieval]]
