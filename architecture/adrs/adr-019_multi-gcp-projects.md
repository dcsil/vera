# ADR 019: Multi-Project Setup for GCP Free Tier Utilization

## Context
Our backend currently spans multiple GCP organizations and projects (Cloud Run, Firestore, Artifact Registry). This setup was chosen to leverage **free tier credits** and minimize costs during early development. However, maintaining multiple projects adds management complexity, fragmented IAM permissions, and deployment friction.

## Decision
Continue using multiple GCP projects temporarily for cost efficiency. In parallel, evaluate a future **migration strategy** or automation layer to centralize resources under a single billing account once cost optimization is less critical.

## Status
Accepted — 2025-10-14

## Consequences
- **Cost Savings:** Free-tier usage across multiple projects delays expenses.  
- **Operational Overhead:** Harder to manage service accounts, permissions, and environment variables.  
- **Future Migration Needed:** Will require consolidation and cleanup before scaling production.
