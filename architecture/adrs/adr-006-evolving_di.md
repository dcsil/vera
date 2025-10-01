## ADR 007: Digital Identity — Eventing (Pub/Sub) & Embeddings (OpenAI in Firestore)

## Context
Our Digital Identity (DI) must update quickly from user actions (bookmarks, likes, group votes) while keeping foreground requests fast. DI also relies on high-quality vector embeddings to power matching and ranking. We need an approach that balances latency, cost, and MVP simplicity, with clear upgrade paths if scale or quality demands increase.

### Options

#### A) Eventing (how DI updates are triggered/applied)
- **Synchronous writes:** Update DI on the request path.
  - Pros: immediate consistency; simpler mental model.
  - Cons: adds latency to user requests; failures block UX; tangled retries/idempotency in foreground.
- **Periodic batch jobs:** Aggregate actions and refresh DI on a schedule.
  - Pros: minimal coupling to request path; easier bulk processing.
  - Cons: stale personalization between runs; poor UX for a feed-style app.
- **Event-driven via Pub/Sub (chosen):** Publish user actions; subscribers update DI asynchronously.
  - Pros: low latency on the request path; near-real-time DI; natural place for retries/dead-letters.
  - Cons: eventual consistency; requires idempotent consumers and monitoring.

#### B) Embeddings (how vectors are produced)
- **OpenAI embeddings (chosen):**
  - Pros: strong quality; fast to integrate; good default for cold start.
  - Cons: vendor cost/quotas; external dependency.
- **Vertex AI text embeddings:**
  - Pros: stays within GCP; potential for unified IAM/billing; competitive quality.
  - Cons: integration change; quality/cost needs evaluation against our workloads.
- **Self-hosted/open-source (e.g., bge, e5, jina):**
  - Pros: cost control; full control over models and privacy.
  - Cons: infra/ops burden; maintenance; hardware costs; slower to MVP.

#### C) Vector Storage & Retrieval (where vectors live, how we search)
- **Embed in Firestore DI docs (chosen for MVP):**
  - Pros: simplest; no extra infra; co-located with DI attributes; fine for small/medium recall.
  - Cons: limited vector query capabilities; may require app-side re-rank or small candidate sets.
- **Relational + pgvector (Cloud SQL/AlloyDB):**
  - Pros: proper ANN indexes; SQL joins with structured catalog.
  - Cons: additional ops; migration complexity.
- **Vertex Matching Engine / managed vector DB (Pinecone/Weaviate/Milvus):**
  - Pros: scalable ANN; high recall/latency SLAs.
  - Cons: added cost, vendor lock-in/ops; more moving parts.

## Decision
- **Eventing:** Use **Google Pub/Sub** to publish user actions; a DI updater subscriber writes changes to **Firestore** asynchronously (eventual consistency tolerated by the UI).
- **Embeddings:** Use **OpenAI embeddings** for the MVP to accelerate delivery and quality; cache results where sensible.
- **Storage:** Store vectors **within Firestore DI documents** alongside graph/attributes for now. If recall/scale or latency becomes a constraint, evaluate **pgvector** (Cloud SQL/AlloyDB) or **Vertex Matching Engine**.

## Status
Accepted — 2025-10-01.  
**Supersedes:** prior drafts ADR 007 (Eventing) and ADR 008 (Embeddings) by merging them into a single DI ADR.

## Consequences
- **Pros**
  - Foreground requests stay fast; DI refreshes near real-time via Pub/Sub.
  - High-quality embeddings with minimal integration effort.
  - Lowest-complexity storage for MVP; fewer moving parts.
- **Cons / Mitigations**
  - Eventual consistency in DI → design UI/UX tolerant to short delays; monitor subscriber lag; use dead-letter queues and idempotency keys.
  - Vendor cost/limits for embeddings → add caching and batch updates; monitor usage/cost.
  - Firestore vector storage limits → maintain a migration plan to pgvector or a managed vector service if candidate retrieval/recall becomes a bottleneck.
