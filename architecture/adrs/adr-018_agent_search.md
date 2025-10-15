# ADR 018: Using Agent-Based Search Instead of Semantic Search

## Context
We evaluated two methods for implementing restaurant search:
- **Semantic search (vector similarity):** Fast and scalable but limited in interpretability and query customization.  
- **Agent-based fuzzy search (chosen):** Uses an LLM agent to interpret user intent and map fuzzy, natural-language queries to dataset fields.

Given our dataset size (<5k) and early-stage MVP, runtime is acceptable, and interpretability is higher with an agent-based approach.

## Decision
Adopt an **agent-driven fuzzy search** system to process natural-language queries and retrieve relevant restaurants dynamically from our dataset.

## Status
Accepted — 2025-10-14

## Consequences
- **Enhanced Query Flexibility:** Handles ambiguous or multi-factor queries (“quiet Italian spots good for dates”).  
- **Higher Interpretability:** Easier to debug and refine than dense embeddings.  
- **Tradeoffs:** Slightly slower response time; not ideal for large-scale retrieval.
