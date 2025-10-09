## ADR 017: Firebase Integration — User Authentication & Firestore Database

## Context
We need a reliable backend service to manage user accounts (sign-in, onboarding, and saved preferences) and to store restaurant metadata, search queries, and user interactions.
### Options

- **Firebase Authentication + Firestore (chosen)** — Granular read/write rules and scalable NoSQL store. Flexible schema allows for dynamic addition of new restaurant attributes and user-specific fields without schema migrations.
- **Custom Node.js + PostgreSQL backend** — Fully customizable and relational, but requires hosting, database management, and manual authentication/security handling.
- **Supabase** — Easier SQL querying and open-source, but weaker real-time syncing and offline caching capabilities compared to Firebase.

## Decision
Adopt Firebase Authentication for user signup/sign-in and Firestore as the main data layer for restaurant info, user search history, and session caching. Auth tokens will gate Firestore access through role-based security rules to minimize data exposure.

## Status
Accepted — 2025-10-08

## Consequences

- Rapid onboarding and consistent auth across devices.
- Firestore provides real-time updates and offline persistence for a smoother mobile-style UX.
- Limited query expressiveness and higher long-term cost if scaling beyond the free tier.
- Need to periodically review security rules to prevent unauthorized read/write access.
