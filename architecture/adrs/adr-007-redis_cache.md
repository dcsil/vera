## ADR 010: Caching — Redis for Hot Queries and Feed Latency

## Context
The app presents a TikTok-style feed; low latency and smooth scrolling are critical.

### Options
- No cache; rely solely on databases
- In-process application cache
- Redis cache

## Decision
Use **Redis** to cache hot queries (popular restaurants, recent recommendation results, repeated searches). Establish TTLs and invalidate from Pub/Sub DI updates and Restaurant Fetching refreshes.

## Status
Accepted — 2025-10-01.

## Consequences
- Improved p95/p99 latency for feed loads.
- Additional infra component to operate and monitor.
- Requires robust keying strategy and invalidation rules.
