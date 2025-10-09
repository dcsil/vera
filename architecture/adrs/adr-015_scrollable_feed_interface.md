## ADR 019: Scrollable Feed Interface — Focused Exploration & Efficient Data Loading

## Context

To display restaurant recommendations in a clear, mobile-friendly format, we needed to decide between two primary presentation models: a paginated card view (swipe or tab-based navigation) or a continuous scrollable feed. The design must balance user focus, cognitive load, and data loading efficiency while aligning with our goal of delivering a lightweight, visually engaging MVP.

## Options

- **Scrollable vertical feed (chosen)** — Users browse a continuous list of restaurant cards with images, rationale text, and badges. Enables focused exploration, natural scrolling gestures, and efficient incremental data loading.
- **Paginated card (carousel) view** — Allows viewing one restaurant at a time (similar to Tinder or TikTok UI), offering strong visual focus but limiting comparison and requiring repeated context switching.
- **Grid or tabbed layout** — Displays multiple venues simultaneously but can overwhelm users and dilute rationale visibility on small screens.

## Decision

Adopt a scrollable vertical feed that displays one to two restaurant cards at a time, with continuous scrolling and lazy loading. This design emphasizes focus on each recommendation while allowing rapid exploration of multiple venues without extra taps.
Flutter’s built-in ListView and ScrollController enable smooth rendering and support incremental loading of restaurant data from Firestore, minimizing memory use and improving performance on mobile devices.

## Status

Accepted — 2025-10-08

## Consequences

- Improved Focus and Flow: The scroll format helps users concentrate on one restaurant at a time without abrupt transitions, increasing attention to rationale text and imagery.
- Efficient Data Handling: Incremental data loading (infinite scroll) reduces initial loading time and memory consumption.
- Consistent UX: Aligns with familiar social app patterns (e.g., Google Maps, Instagram Explore), improving discoverability and engagement.
- Tradeoffs: Less effective for side-by-side comparison; requires attention to scroll performance and placeholder handling for unloaded items.
