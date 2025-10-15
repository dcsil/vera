# ADR 017: Restricting Dataset to Toronto Restaurants Only

## Context
The Kaggle dataset initially included restaurants across the GTA (~10,000 entries). Many entries were outside our target launch city and contained inconsistent metadata (missing photos, cuisine tags, or location info).

## Decision
Filter and retain only **Toronto-based restaurants**, reducing the dataset from ~10,000 to fewer than 5,000 entries. Implement a flagging system for missing or low-quality metadata (e.g., missing rating, category, or address) to exclude or enrich later.

## Status
Accepted — 2025-10-14

## Consequences
- **Improved Data Quality:** Fewer but cleaner entries for recommendations.  
- **Simplified Launch Scope:** Easier to validate MVP performance within a single city.  
- **Scalability Challenge:** Future city expansions will require similar cleaning workflows.
