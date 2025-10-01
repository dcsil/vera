## ADR 014: Tavily API Integration — SERP/Enrichment

## Context
Cards benefit from lightweight, recent web context (e.g., press mentions, menu highlights, updates like reopenings). We must control cost/latency and avoid blocking core recommendations.

### Options
- **Tavily API** for curated, LLM-friendly search (chosen)
- Direct search scraping (fragile; TOS risk)
- No enrichment (simpler but lower perceived quality)

## Decision
Use **Tavily** from the **SERP/ReAct Enrichment Agent** only **after** candidates are shortlisted to cap spend. Extract short snippets/links, summarize client-side, and cache with short TTLs. Never block core results on enrichment; degrade gracefully.

## Status
Accepted — 2025-10-01.

## Consequences
- Improves freshness/quality with minimal engineering.
- Must enforce per-request and per-user/day budgets; monitor spend.
- Cache normalized snippets (Redis/Firestore) for hours–days TTL.
- If Tavily errors/quotas, omit enrichment section without failing the request.
