# FluxCache Architecture

This document describes the high-level architecture of FluxCache.

## Overview
FluxCache is a high-performance caching layer designed for LLM responses.

## Components
- **Core Engine**: Handles cache logic and eviction policies.
- **Storage Layer**: Interface for different storage backends (Redis, In-memory).
- **Embedding Engine**: Manages vector embeddings for semantic search.
- **API Wrapper**: Provides hooks for popular LLM clients.

## Data Flow
1. Request received
2. Compute embedding
3. Semantic search in cache
4. Return cached result or call LLM
5. Store new response in cache
