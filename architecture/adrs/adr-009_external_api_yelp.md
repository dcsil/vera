## ADR 012: Yelp API Integration — Restaurant Metadata & Photos

## Context
We need reliable restaurant metadata (name, categories, price, rating/counts, hours, geo) and photos to enrich results for Toronto venues and beyond. Freshness, quota management, and TOS compliance matter.

### Options
- Use **Yelp Fusion API** (chosen)
- Use **Google Places API** (chosen)
- Build scrapers/ingest pipelines (high maintenance, TOS risk)
- Buy third-party datasets (costly, may lack freshness/media)
- Scrape search/maps

## Decision
Integrate **Google Places API** in the **Restaurant Fetching Service** alongside Yelp. Normalize to a shared schema, track provider provenance, and **merge/deduplicate** businesses (geohash + name similarity + phone/URL). Prefer cached and canonical records; keep provider IDs for later refreshes.


## Status
Accepted — 2025-10-01.

## Consequences
- Better coverage and resilience; higher engineering complexity for merge/dedup.
- Quota handling and costs across two providers.
- Use Redis for hot results; Firestore/Cloud SQL for canonical store + update timestamps.
- Enforce attribution and photo-usage policies.
