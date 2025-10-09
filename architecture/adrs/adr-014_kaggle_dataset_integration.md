## ADR 014: Kaggle Dataset Integration — Toronto Restaurant Data via Google Cloud

## Context
To enhance local recommendations, mitigate API rate limits, and develop a working end-to-end analysis platform for our MVP, we plan to ingest an offline restaurant dataset from Kaggle into a managed cloud environment. This dataset includes restaurant names, cuisines, ratings, and coordinates specific to Toronto.

## Options
- **Kaggle → Google Cloud Storage + BigQuery pipeline (chosen)** — scalable data pipeline with SQL querying and export to Firestore.
- **Local CSV ingestion** — simpler, but harder to maintain or scale; not shareable among collaborators.
- **API-only approach (Google Places/Yelp)** — always fresh data, but limited access and subject to request caps.

## Decision
Upload the Kaggle Toronto Restaurants dataset to Google Cloud Storage and process it via BigQuery, allowing clean, structured data to be exported to Firestore. This serves as our fallback source when external APIs are rate-limited or unavailable.

## Status
Accepted — 2025-10-06

## Consequences
- Enables faster prototype testing without relying on external APIs.
- Supports consistent restaurant metadata and reproducible results.
- Requires periodic updates to remain current with real-world restaurant changes.
- Introduces minor setup overhead and potential cloud cost management.
