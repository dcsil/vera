## ADR 006: Multi-Agent Systems — LangGraph over CrewAI (considered AutoGen)

## Context
The recommendation pipeline coordinates specialized agents (fetch, analyze, rank, enrich). We need predictable runtimes, explicit control flow, easy retries/timeouts, and clear state passing—without heavy platform overhead for the MVP.

### Options
#### A) CrewAI
- **Pros:** Quick to prototype “role” and “task” patterns; minimal boilerplate to get agents collaborating.
- **Cons:** Less deterministic control flow; observed longer runtimes in our tests; harder to express complex branching and fine-grained timeouts/retries.
- **Fit:** Exploration and simple agent teams; less ideal for latency-sensitive serving paths.
#### B) LangGraph (chosen)
- **Pros:** Graph-based orchestration (nodes/edges) with explicit state; good for parallel branches, guards, retries, timeouts, and tool calls. Integrates with LangChain ecosystem, streaming, and memory patterns. Predictable control flow helps debugging and SLOs.
- **Cons:** Requires light upfront modeling of the graph; still evolving APIs.
- **Fit:** Production-lean MVP where determinism, observability, and fast iteration matter.
#### C) AutoGen (Microsoft)
- **Pros:** Strong multi-agent abstractions; chat-centric collaboration patterns; good for research/IDEation loops and tool-use demos.
- **Cons:** Conversation-first paradigm can be less ergonomic for strict, low-latency pipelines; extra adaptation needed for stateful branching, time-boxed steps, and service integration.
- **Fit:** R&D workflows and autonomous “brainstorming” agents; less ideal as our serving orchestrator.

## Decision
Adopt **LangGraph** for the MVP recommendation pipeline. It gives us explicit, testable graphs for fetch → analyze → rank → enrich, supports parallelism and guarded edges, and plays well with LangChain components we already use (embeddings, tools, retrievers). We keep **CrewAI** and **AutoGen** in the toolbox for experimentation and offline workflows.

## Status
Accepted — 2025-10-01.

## Consequences
- **Pros:** Predictable control flow and latency; simpler debugging; straightforward retries/timeouts; easy to compose new agents as nodes.
- **Cons/Watchouts:** Track LangGraph API changes; invest in a small test harness per graph; document state schema between nodes.
- **Migration Path:** If constraints tighten or features outgrow LangGraph, we can (a) replace specific nodes with services, (b) introduce a custom micro-orchestrator for hot paths, or (c) delegate ideation/research tasks to AutoGen/CrewAI while keeping LangGraph for serving.
