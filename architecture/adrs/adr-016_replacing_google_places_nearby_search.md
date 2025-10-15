# ADR 016: Replacing Google Places Nearby Search with Kaggle Dataset Query

## Context
Google Places API’s Nearby Search endpoint provides extensive restaurant data but is not optimized for our needs. It is costly at scale, provides limited filtering for dine-in vs. fast-food restaurants, and introduces latency. Since our app focuses on curated dine-in recommendations rather than general discovery, Places API returns too much noise (e.g., chains, coffee shops, fast food).

## Decision
Use our pre-curated **Kaggle dataset of Toronto restaurants** as the primary source for restaurant retrieval and exploration. This dataset is cleaned, structured, and suitable for filtering within our Firestore database.

## Status
Accepted — 2025-10-14

## Consequences
- **Reduced Costs:** Eliminates API charges for bulk queries.  
- **Faster Querying:** Local database queries are faster than remote API calls.  
- **Less Data Noise:** Improves recommendation quality by removing irrelevant categories.  
- **Tradeoffs:** Dataset may lack real-time data or reviews compared to Google’s API.
