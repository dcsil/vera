## ADR 003: Frontend — Flutter Mobile-First, Web Optional

## Context
Dining decisions are predominantly mobile. We want one codebase to deliver iOS/Android now and preserve the option to expand to web later. Team familiarity matters for MVP speed.

### Options
- Native iOS + Android
- React Native + separate web app
- Flutter mobile-first with optional web

## Decision
Use **Flutter** to deliver iOS/Android first, with optional web compilation. This matches the mobile use case, keeps one codebase, and leverages team familiarity for faster MVP delivery.

## Status
Accepted — 2025-10-01.

## Consequences
- Single codebase, faster delivery.
- Web builds may require additional UI tuning.
- Larger binary sizes than fully native apps.
