## ADR 004: Architecture Style — Lightweight Microservices on Cloud Run

## Context
Most features (auth, profiles, groups, bookmarks) are small and separable. Our core IP is the recommendation pipeline. We need modularity without over-engineering.

### Options
- Monolith
- Lightweight microservices on Cloud Run
- Full microservices on GKE with service mesh

## Decision
Adopt **small, focused services on Cloud Run**: Auth, Profile/DI, Search, Recommendation, Restaurant Fetcher, Group, Bookmark/Like. Keep boundaries clear; avoid Kubernetes/service mesh for MVP.

## Status
Accepted — 2025-10-01.

## Consequences
- Independent scaling and deployments.
- Clear ownership and fault isolation.
- Some overhead in API contracts and CI/CD per service.
