## ADR 016: Meta API Integration — Optional Social Signals

## Context
Optional social signals (liked venue posts, check-ins, saved spots) can improve personalization and group consensus, but come with higher privacy/compliance sensitivity.

### Options
- **Meta Graph APIs** with explicit opt-in (chosen, optional)
- Scraping (against TOS)
- Omit social context (simpler; less signal)

## Decision
Add a **Social Context Adapter** that, when a user connects Meta, fetches coarse venue-related signals and maps them to internal venue IDs/categories. Do **not** store raw posts/captions; minimize retained personal data.

## Status
Accepted — 2025-10-01.

## Consequences
- Potential lift in personalization and group overlap detection.
- Highest sensitivity integration: narrow scopes, transparent consent, easy disconnect, and purge controls.
- Enforce platform policies; implement rate limits and graceful degradation.
