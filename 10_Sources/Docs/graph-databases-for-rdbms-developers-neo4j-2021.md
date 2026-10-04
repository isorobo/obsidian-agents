---
type: source
status: draft
created: 2026-08-12
title: "The Definitive Guide to Graph Databases for the RDBMS Developer"
authors:
- Michael Hunger
- Ryan Boyd
- William Lyon
organisation: "Neo4j"
source_type: docs
venue: "Neo4j ebook"
url: TBD
year: 2021
date_published: 2021
anthropic: false
topic:
- topic/retrieval
- topic/architectures
tags: [graph-database, neo4j, cypher, data-modelling, relational-database, index-free-adjacency]
authored_by: agens
nlm_id: 
nlm_skip: false
watchlist_channel: 
af_targets:
- none
wiki_indexed: '2026-10-04T03:01:49Z'
wiki_hash: fed8b973b18576c3b9cee3a0d5f53d1ec061994b6a8bd550a2ec32d5d11e6dc3
---

# The Definitive Guide to Graph Databases for the RDBMS Developer

> Full citation: Hunger, M., Boyd, R. and Lyon, W. "The Definitive Guide to Graph Databases for the RDBMS Developer." Neo4j ebook, Neo Technology, 2021. neo4j.com.

## Summary

This 34-page Neo4j ebook teaches graph databases to a developer who already knows relational databases. It runs in six chapters plus a conclusion. Chapter 1 sets out where the relational model strains under connected data: JOIN explosion, recursive JOINs, frequent schema changes, slow queries despite tuning, and pre-computed results. Chapter 2 defines a graph as nodes and relationships, defines a graph database as a CRUD system over that model, and names native graph storage and native graph processing as the two properties that matter. Chapter 3 compares relational and graph modelling through a data centre management domain, and gives a 10-point checklist for converting a relational schema into a property graph. Chapter 4 contrasts SQL with Cypher across two worked queries. Chapter 5 sets out three deployment paradigms for pairing a graph database with an RDBMS, then covers extraction and import through `LOAD CSV`, the command-line bulk loader, and the transactional Cypher HTTP endpoint. Chapter 6 covers connection paths: the Neo4j Browser, the REST API, language drivers, JDBC, and Spring Data Neo4j. The intended reader is an RDBMS developer or architect assessing whether to add or substitute a graph store, and the tone is vendor advocacy backed by worked models and code.

## Key Concepts

- Relational databases store entities well and relationships poorly. The name derives from Codd's mathematical "relation", a table, and not from relationships between data.
- Foreign keys and JOIN tables encode relationships as model-level metadata. That metadata serves the database, not the user, and obscures the domain.
- JOINs compute at query time by matching primary and foreign keys. The cost grows as queries add tables and depth.
- A graph holds two elements: a node, which represents an entity, and a relationship, which represents how two nodes associate.
- Relationships in a graph database are first-class entities. The application infers no connection through foreign keys or out-of-band processing such as MapReduce.
- Native graph storage designs the store around the graph. Non-native storage layers a graph over a relational or object-oriented engine and adds latency.
- Index-free adjacency means connected nodes point at each other in the store. Each node holds a list of relationship records, typed and directed, that can carry properties.
- Pre-materialised relationships turn a JOIN into a traversal, a constant time operation. Query time holds steady as the dataset grows.
- Normalised relational models rarely perform well enough in production. Denormalisation duplicates data to buy speed and distorts the user's model to suit the engine.
- Relational change arrives as a migration. Code refactorings take minutes; database refactorings take weeks or months, with downtime for schema changes.
- A graph model needs no normalisation or denormalisation step. The whiteboard sketch is the stored structure.
- Cypher expresses graph patterns as ASCII art, so the query mirrors the diagram the team drew.
- Three deployment paradigms exist: full migration, split by workload, and full duplication across both stores. The second and third are polyglot persistence.

## Terminology

- **Node**: an entity in the graph. A person, place, thing, or category.
- **Relationship**: a named, directed connection between two nodes. It may carry properties.
- **Label**: a role marker on a node. One node can carry several, such as a specific `Server` label and a general `Asset` label.
- **Property**: a key-value pair on a node or a relationship.
- **Index-free adjacency**: native graph processing in which connected nodes point at each other in the store, removing the index lookup.
- **Native graph storage**: a store built for graphs, as against a graph layered over a relational or object-oriented database.
- **SQL strain**: the guide's label for the five symptoms of an RDBMS handling connected data.
- **Polyglot persistence**: using more than one data store, each for its strength.
- **Cypher**: a declarative, open, multi-vendor graph query language. Neo4j sponsored it; the openCypher project widened it beyond Neo4j.
- **`LOAD CSV`**: the Cypher keyword that reads CSV files from an HTTP or file URL and creates or updates graph structure per row.
- **`neo4j-import`**: the command-line bulk loader for initial database population.
- **Neo4j-OGM**: the object graph mapping library that Spring Data Neo4j integrates.

## Architecture and Implementation

The guide maps a relational schema onto a property graph through a fixed checklist. Each entity table becomes a node label. Each row in an entity table becomes a node. Columns on those tables become node properties. Technical primary keys drop out; business primary keys stay and take unique constraints, and frequent lookup attributes take indexes. Foreign keys become relationships, then the foreign key columns go. Columns holding default values go, since the graph stores no default. Denormalised and duplicated data in a table splits out into separate nodes. Indexed column names such as `email1`, `email2`, and `email3` signal an array property. JOIN tables become relationships, and the columns on a JOIN table become relationship properties.

The guide works the mapping twice. The first pass covers a small organisational domain of `Persons` and `Projects` inside an `Organization` with several `Departments`. The second pass covers a data centre management domain: applications, database servers, virtual machines, servers, racks, load balancers, and a user. On the relational side the model passes through a whiteboard sketch, an entity-relationship diagram, a normalised table design, and then a denormalisation pass for access patterns. Each step widens the gap between the conceptual model and the physical layout. The guide notes that an E-R diagram is itself a graph, and that it permits only single, undirected relationships between entities.

On the graph side the process stops after enrichment. The team keeps the whiteboard structure, adds labels for roles, properties for attributes, and named directed relationships for connections. The finished data centre graph gives most nodes two labels, a type label such as `Database`, `App`, or `Server`, and a general `Asset` label, so one query can target a type and another can sweep every asset. Transactions group node and relationship updates into an ACID operation, with write-ahead logging and recovery after abnormal termination. No fixed aggregate boundary exists, so the application sets the scope of an update at read or write time.

For deployment, the guide sets out three paradigms. A team migrates every table into the graph in one bulk load. A team keeps the RDBMS for tabular workloads and routes JOIN-heavy and relationship workloads to the graph. A team duplicates all data into both stores and queries whichever fits. The guide names no correct choice and points the reader at application goals, frequent use cases, and common queries.

Import runs in two stages: extract, then load. Extraction dumps tables or query results to CSV, or pulls data through JDBC or another driver. A timestamp or updated flag drives a repeating sync. The guide warns that relational databases handle bulk export poorly, and cites a customer whose MySQL export took three days against a Neo4j import of three hours. Loading has three routes. `LOAD CSV` reads single-table, denormalised, or joined CSV files, converts and filters values during import, matches existing nodes, creates or merges nodes and relationships, sets or removes labels and properties, and caps transaction size to hold memory down. The `neo4j-import` bulk loader parallelises across CPUs and disk, reaches one million records per second, handles several billion nodes, and serves initial population alone. The transactional Cypher HTTP endpoint runs parameterised statements from any driver or HTTP client, and holds a transaction open across requests.

Connection paths follow from that. The Neo4j Browser answers on `localhost:7474` and fills the role SQL*Plus fills for an RDBMS. The REST API posts one or more Cypher statements with parameters per request, keeps transactions open, chooses result formats, and introspects the database. Language drivers wrap the same APIs for Java, .NET, JavaScript, Python, Ruby, PHP, R, Go, Clojure, Perl, and Haskell. Cypher is textual, parameterisable, and returns tabular results, so a Neo4j-JDBC driver exposes it through the JDBC APIs and lets an existing ETL or business intelligence tool reach the graph. Spring Data Neo4j sits above Neo4j-OGM and supplies object graph mapping, Spring conversions, transaction handling, repositories, Spring Data REST, and Spring Boot support.

## Code Examples

The guide carries its argument through side-by-side SQL and Cypher. The first pair lists the employees in the IT Department. SQL walks a JOIN table:

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

The guide measures the Cypher query at half the length of the SQL. The second pair builds a co-purchase recommendation. The Cypher query traverses from a customer to a bought product, out to peer customers, and on to their other products, then filters what the customer already owns:

```cypher
MATCH (u:Customer {customer_id:'customer-one'})-[:BOUGHT]->(p:Product)
      <-[:BOUGHT]-(peer:Customer)-[:BOUGHT]->(reco:Product)
WHERE not (u)-[:BOUGHT]->(reco)
RETURN reco as Recommendation, count(*) as Frequency
ORDER BY Frequency DESC LIMIT 5;
```

Each arrow in that `MATCH` maps to a many-to-many JOIN table with two JOINs, so the query covers six JOINs. The SQL equivalent nests a three-way self-join over `Customer_product_mapping` inside a subquery, adds a `not in` subquery for products already bought, then groups and orders the outer result. The guide measures it at three times the length of the Cypher.

Cypher pattern syntax carries the contrast. Parentheses draw nodes, `(a:Person {name:'Jim'})`. Dashes with angle brackets draw direction, `-[:KNOWS]->`. A colon prefixes a label and a relationship type. Curly braces hold property key-value pairs. A triangle of three mutual friends reads as `(emil)<-[:KNOWS]-(jim)-[:KNOWS]->(ian)-[:KNOWS]->(emil)`. Beyond `MATCH` and `RETURN`, the guide lists `WHERE`, `CREATE`, `CREATE UNIQUE`, `MERGE`, `DELETE`, `REMOVE`, `SET`, `ORDER BY`, `SKIP LIMIT`, `FOREACH`, `UNION`, and `WITH`, and compares `WITH` to piping in Unix.

The import chapter gives a `LOAD CSV` example over a semicolon-delimited `persons.csv` with `name`, `email`, and `dept` columns. It merges a `Person` on email, sets the name on create, matches the `Department` by name, and creates an `EMPLOYEE` relationship. The driver chapter gives a JDBC example: `DriverManager.getConnection("jdbc:neo4j://localhost:7474/")`, a `PreparedStatement` holding a `MATCH (:Person {name:{1}})-[:EMPLOYEE]-(d:Department) RETURN d.name as dept` query, and a `ResultSet` loop that reads the `dept` column. It also shows a raw HTTP call, a `POST` to `/db/data/transaction/commit` carrying a `CREATE (p:Person {name:{name}}) RETURN p` statement with parameters, and the JSON result it returns.

## Best Practices

- Draw a basic graph model on a whiteboard before the first import. Knowing the target model reduces import pain.
- Learn the property graph model, nodes, relationships, labels, properties, and relationship types, before choosing a deployment paradigm.
- Keep business primary keys and drop technical primary keys during conversion. Add unique constraints on the business keys.
- Add indexes on attributes the application looks up often.
- Give a node both a type label and a general label, such as `Server` and `Asset`, so queries can target one type or sweep every instance.
- Choose the deployment paradigm from application goals, frequent use cases, and common queries.
- Sync on a timestamp or an updated flag where the relational and graph stores run side by side.
- Cap transaction size inside `LOAD CSV` to avoid memory exhaustion.
- Run `LOAD CSV` from the Neo4j shell rather than the browser to script imports.
- Reserve `neo4j-import` for initial population. Its optimisations rule out later use.
- Parameterise Cypher statements sent over HTTP or JDBC.
- Disable virus scanners and check the disk schedule before a large write.
- Reach for a language driver rather than raw HTTP for application code.

## Warnings and Anti-Patterns

- Treating a relational database as a store of relationships. It records references through foreign keys and computes the connection at query time.
- A query that JOINs many tables. Complexity and resource use rise together, and response time follows.
- Recursive self-JOINs for hierarchies and trees. The guide names them among the longest SQL queries written.
- Answering slow queries with more hardware. A query needing over 100 cores signals a model problem, and data growth demands still more hardware.
- Pre-computing results from a snapshot. The application serves yesterday's data, and the system computes 100% of the dataset to serve the 1% to 2% a query touches.
- Denormalising for speed. It duplicates data, harms data quality and update behaviour, and binds every developer to a model that no longer matches the domain.
- Assuming the design, normalise, denormalise cycle runs once. Requirements move, and each move costs a migration measured in weeks or months.
- Long SQL statements. Length invites coding mistakes and hides the original developer's intent from the next reader.
- Non-native graph storage and non-native graph processing. Both add index lookups and latency as data volume and query complexity grow.
- Modelling a rich domain with E-R diagrams alone. They allow one undirected relationship between two entities.

## Related Concepts

- [[memory]]
- [[glossary]]
- [[graph-database]]
- [[index-free-adjacency]]
- [[polyglot-persistence]]
- [[knowledge-graph]]
- [[MOC - Architectures]]

## Future Work

The guide states that it scratches the surface and routes the reader onward. Chapter 5 lists further import routes beyond `LOAD CSV`, the bulk loader, and the HTTP endpoint, including a direct RDBMS import tool and a SQL to Neo4j import tool. Chapter 6 covers Neo4j drivers alone and tells readers of other graph databases to consult those communities. The closing resource list points to the Graph Databases for Beginners series, a relational-to-Neo4j developer guide, a white paper on SQL strain, three webinars, the O'Reilly Graph Databases ebook, Learning Neo4j, and Neo4j training. The market projections the guide cites, Forrester on 25% enterprise adoption by 2017 and Gartner on 70% of leading organisations running a graph pilot by the end of 2018, now sit in the past and need current figures.

## References

- Hunger, M., Boyd, R. and Lyon, W. "The Definitive Guide to Graph Databases for the RDBMS Developer." Neo4j ebook, Neo Technology, 2021.
- Publisher site stated in the ebook: https://neo4j.com
- Cited within the guide: "The Top 5 Use Cases of Graph Databases: Unlocking New Possibilities with Connected Data" (Neo4j); the openCypher project; the Cypher Refcard; O'Reilly, "Graph Databases"; "Learning Neo4j".
