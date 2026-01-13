# Development Guide

This guide will help you set up your development environment for FluxCache.

## Prerequisites
- Rust 1.75+
- Docker
- Git

## Setup
1. Clone the repo
2. Run `cargo build`
3. Run tests with `cargo test`

## Environment Variables
- `REDIS_URL`: URL for the Redis instance (default: `redis://127.0.0.1:6379`)

## Testing
We use `cargo-nextest` for faster test execution.
```bash
cargo nextest run
```
