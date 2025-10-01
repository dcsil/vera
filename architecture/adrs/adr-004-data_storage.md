## ADR 005: Data Stores — Firestore (NoSQL) + Cloud SQL (Postgres) + Redis

## Context
We must store evolving user identities (graphs/embeddings), operational app data, and a structured Toronto restaurant dataset, while meeting feed-style latency targets and keeping MVP complexity low.

### Options
#### A) Digital Identity (embeddings, evolving graph-like attributes)
- **Firestore (documents) + embedded vectors**  
  Store DI attributes and vectors in user docs; simple, fast to iterate.
- **Vector DB / ANN service**  
  - pgvector on Cloud SQL / AlloyDB  
  - Milvus
  Pros: native vector search, better recall/scale. Cons: extra infra/cost/ops for MVP.
- **Graph-first store**  
  - Neo4j
  - Google Cloud Spanner (Graph extensions)  
  Pros: explicit graph semantics & traversal. Cons: higher complexity, migration cost.

#### B) Operational App Data (profiles, groups, bookmarks, settings)
- **Firestore (NoSQL documents)**  
  Pros: flexible schema, easy ACLs, great GCP integration.  
- **Cloud SQL / AlloyDB (relational)**  
  Pros: strong consistency, joins. Cons: slower schema evolution for MVP.  
- **Bigtable**  
  Pros: high throughput, wide-column. Cons: overkill, operational burden for MVP.

#### C) Restaurant Catalog / Toronto Dataset (structured, queryable)
- **Cloud SQL (Postgres)**  
  Pros: relational queries (cuisine, price, geo), familiar tooling, pg extensions.  
- **Firestore**  
  Pros: fast doc reads. Cons: complex filters/joins, harder for rich structured queries.

#### D) Caching / Low-Latency Feed
- **Redis (Memorystore)**  
  Pros: sub-ms reads, TTLs, rich data structures.  
- **In-process cache**  
  Pros: simplest. Cons: no cross-instance coherence on Cloud Run.  
- **CDN (Cloud CDN)**  
  Pros: edge cache. Cons: dynamic, user-specific feeds don’t cache well.



## Decision
Adopt a **hybrid** approach aligned to workload shape:
- **Digital Identity & Operational App Data → Firestore (NoSQL)** with embedded vectors for MVP. Keep schemas flexible; emit events to update DI asynchronously.
- **Restaurant Catalog → Cloud SQL (Postgres)** seeded from the Toronto Kaggle dataset; leverage relational filters, indices, and geospatial extensions as needed.
- **Caching → Redis (Memorystore)** for hot queries and feed responses (with strict TTLs and invalidation hooks).

Plan migration paths:
- If vector recall/scale becomes a bottleneck, evaluate **Vertex Matching Engine** or **pgvector** in Cloud SQL/AlloyDB.  

Evaluate **Graph Spanner** or **Bigtable** for DI graphs at scale.

## Status
Accepted — 2025-10-01.

## Consequences
- Flexible schemas and rapid iteration.
- Strong relational capabilities where needed.
- Additional cache infra to operate; clear invalidation rules required.
