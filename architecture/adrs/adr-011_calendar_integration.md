## ADR 015: Google Calendar Integration — Read-Only Context

## Context
Calendar context (times, coarse locations) can trigger smarter, timely suggestions (e.g., “after the 6 pm meeting near X”). Privacy and consent are critical.

### Options
- **Google Calendar API (read-only)** with user consent (chosen)
- Manual user input (higher friction)
- Read-write scopes (unnecessary and riskier)

## Decision
Create a **Calendar Adapter** service to fetch **read-only** events for opted-in users. Derive only **time windows** and **coarse location** features; do not persist raw event bodies unless a user explicitly enables persistent context.

## Status
Accepted — 2025-10-01.

## Consequences
- Better, context-aware suggestions with minimal data retention.
- Use least-privilege scopes; build clear consent UX and easy revocation.
- On revocation or errors, skip calendar-aware logic without failing the request.
