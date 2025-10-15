# ADR 020: Selective Google Places API Calls with Firebase Caching

## Context
Google Places API costs increase rapidly beyond 5,000 calls per month, making it impractical for mass data ingestion. However, some fields (e.g., photos, live status, summaries) remain valuable for specific restaurants queried by users.

## Decision
Limit Places API usage to **on-demand lookups** for restaurants fetched from our Kaggle/Firestore dataset. Cache the enriched metadata (photos, reviews, summaries) in Firebase for reuse. This hybrid approach balances freshness with cost efficiency.

## Status
Accepted — 2025-10-14

## Consequences
- **Cost Control:** Reduces Places API usage by >80%.  
- **Offline Resilience:** Cached data ensures continued service when API is unavailable.  
- **Improved Latency:** Avoids redundant external calls.  
- **Tradeoffs:** Cached data may become stale; requires periodic refresh or backup DB outside Google ecosystem.
