## ADR 002: Backend — Python + FastAPI on Cloud Run

## Context
The backend must support rapid MVP development, straightforward HTTP APIs, and strong AI/ML library support for embeddings and agent orchestration. 

### Options
- Node.js + Express on Cloud Run
- Go + net/http on Cloud Run
- Python + FastAPI on Cloud Run

## Decision
Use **Python** with **FastAPI** deployed to **Google Cloud Run**. Python provides a mature AI ecosystem (LangChain, LangGraph, embeddings clients). FastAPI offers high developer velocity, async support, and good performance for I/O-bound services. Cloud Run gives autoscaling, containerized deploys, and low ops overhead.

## Status
Accepted — 2025-10-01.

## Consequences
- Rapid iteration with rich library support.
- Must manage concurrency (async/await) and cold starts.
- Container sizing and startup optimization required.
