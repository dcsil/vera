## ADR 011: API Gateway and Load Balancer — Included in Design, Optional for MVP

## Context
We want an upgrade path to production-grade routing, quotas, and auth offloading without blocking MVP delivery.

### Options
- Exclude gateway/LB for MVP; add later
- Include in architecture and enable pragmatically
- Mandate gateway/LB from day one

## Decision
Design for **Cloud Load Balancing + API Gateway**, but keep them optional during early MVP. Enable when traffic, partners, or security posture requires more control.

## Status
Accepted — 2025-10-01.

## Consequences
- Minimal upfront complexity for MVP.
- Smooth path to enterprise-grade controls.
- Maintain Terraform/IaC scaffolding to enable quickly.
