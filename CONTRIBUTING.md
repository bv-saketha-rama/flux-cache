# Contributing to FluxCache

Thank you for your interest in contributing! 

We're on a mission to **stop LLM applications from bleeding money** on duplicate queries. FluxCache is solving the 4 critical bottlenecks in LLM caching:
1. **Redundant Query Tax** - Semantic caching for massive cost savings
2. **Streaming Waste** - World's first streaming-aware cache
3. **Static Thresholds** - ML-powered adaptive learning
4. **Observability Gap** - Real-time cost tracking

Every contribution helps make LLM applications faster, cheaper, and more observable. See our [Vision](https://github.com/bv-saketha-rama/FluxCache/issues/2) for the full roadmap.

## Table of Contents
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)
- [Issue Guidelines](#issue-guidelines)
- [Code Style](#code-style)

## Getting Started

### Prerequisites
- Rust 1.75 or higher
- Docker & Docker Compose
- Git

### Setup Development Environment

1. **Fork and clone the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/fluxcache.git
   cd fluxcache
   ```

2. **Install Rust toolchain**
   ```bash
   rustup update stable
   rustup component add rustfmt clippy
   ```

3. **Start Redis**
   ```bash
   docker-compose up -d
   ```

4. **Build and test**
   ```bash
   cargo build --workspace
   cargo test --workspace
   ```

5. **Verify everything works**
   ```bash
   cargo clippy --workspace
   cargo fmt --all -- --check
   ```

## Priority Contribution Areas

Looking for high-impact contributions? Focus on these areas aligned with our [roadmap](https://github.com/bv-saketha-rama/FluxCache/issues/2):

### Phase 1: Foundation (v0.1.0)
- **Semantic Caching Core** - Embedding generation, cosine similarity, Redis integration
- **Testing** - Unit tests, integration tests, benchmarks
- **Documentation** - API docs, examples, architecture guides

### Phase 2: Innovation (v0.2.0)
- **Streaming Cache** - Hierarchical caching, partial response persistence
- **ML Adaptive Thresholds** - XGBoost model, feedback loop, online learning
- **Performance** - Latency optimization, memory efficiency

### Phase 3: Production (v0.3.0)
- **TUI Dashboard** - Real-time metrics, cost tracking, heatmaps
- **Observability** - Prometheus metrics, logging, alerting
- **Production Hardening** - Error handling, resilience, security

Check [open issues](https://github.com/bv-saketha-rama/FluxCache/issues) labeled with `good-first-issue`, `help-wanted`, or `roadmap`.

## Development Workflow

### 1. Create a Branch
Always create a new branch for your work:
```bash
git checkout -b feat/your-feature-name
# or
git checkout -b fix/issue-123
```

Branch naming conventions:
- `feat/` - New features
- `fix/` - Bug fixes
- `docs/` - Documentation changes
- `refactor/` - Code refactoring
- `test/` - Adding tests
- `chore/` - Maintenance tasks

### 2. Make Your Changes
- Write clean, readable code
- Add tests for new functionality
- Update documentation as needed
- Keep commits focused and atomic

### 3. Test Your Changes
```bash
# Run tests
cargo test --workspace

# Check formatting
cargo fmt --all -- --check

# Run linter
cargo clippy --workspace -- -D warnings

# Run specific package tests
cargo test --package fluxcache-core
```

### 4. Commit Your Changes
See [Commit Guidelines](#commit-guidelines) below.

### 5. Push and Create PR
```bash
git push origin feat/your-feature-name
```
Then open a Pull Request on GitHub.

## Commit Guidelines

We follow [Conventional Commits](https://www.conventionalcommits.org/) specification.

### Format
```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation only
- `style`: Code style changes (formatting, semicolons, etc.)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `chore`: Maintenance tasks
- `ci`: CI/CD changes

### Examples
```bash
feat(cache): add streaming response caching

Implements hierarchical caching for streaming LLM responses.
Saves partial responses at sentence boundaries.

Closes #42

***

fix(embedding): handle empty string inputs

Previously crashed on empty strings, now returns early with error.

Fixes #38

***

docs(readme): update installation instructions

Added Docker setup steps and troubleshooting section.
```

### Scope (Optional)
- `cache` - Caching logic
- `embedding` - Embedding engine
- `storage` - Storage backends
- `api` - HTTP API
- `cli` - Command-line interface
- `core` - Core library

## Pull Request Process

### Before Submitting
- [ ] Code compiles without warnings
- [ ] All tests pass
- [ ] Added tests for new functionality
- [ ] Updated documentation
- [ ] Followed code style guidelines
- [ ] Commits follow conventional commits
- [ ] PR title follows conventional commits format

### PR Title Format
Same as commit format:
```
feat(cache): add adaptive threshold learning
fix(api): resolve timeout issue in streaming endpoint
```

### PR Description Template
Our PR template will auto-populate. Fill in all sections:
- What problem does this solve?
- How did you solve it?
- How to test?
- Related issues

### Review Process
1. CI must pass (all checks green)
2. At least one maintainer approval required
3. No unresolved conversations
4. Squash and merge into main

### After Merge
- Delete your branch
- Update your fork
- Close related issues (if not auto-closed)

## Issue Guidelines

### Before Creating an Issue
- Search existing issues to avoid duplicates
- Check if it's already fixed in `main` branch
- Provide clear reproduction steps

### Issue Types
Use our issue templates:
- **Bug Report** - Something isn't working
- **Feature Request** - Suggest a new feature
- **Question** - Ask for help (or use Discussions)

### Good Issue Characteristics
- Clear, descriptive title
- Complete reproduction steps
- Expected vs actual behavior
- Environment details (OS, Rust version)
- Code samples or logs

## Code Style

### Rust Style Guide
Follow the [Rust Style Guide](https://doc.rust-lang.org/nightly/style-guide/):
- Use `rustfmt` (enforced by CI)
- Maximum line length: 100 characters
- Use meaningful variable names
- Add doc comments for public APIs

### Documentation
```rust
/// Embeds the given text into a vector representation.
///
/// # Arguments
/// * `text` - The input text to embed
///
/// # Returns
/// A 384-dimensional vector embedding
///
/// # Errors
/// Returns `FluxCacheError::EmbeddingError` if text is empty or model fails
///
/// # Example
/// ```
/// let embedding = embed_text("Hello world")?;
/// assert_eq!(embedding.len(), 384);
/// ```
pub fn embed_text(text: &str) -> Result<Vec<f32>> {
    // implementation
}
```

### Error Handling
- Use `Result<T>` for recoverable errors
- Use descriptive error messages
- Add context to errors: `.context("Failed to load model")`
- Don't use `unwrap()` or `expect()` in library code

### Testing
```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_embed_text_success() {
        let result = embed_text("test");
        assert!(result.is_ok());
        assert_eq!(result.unwrap().len(), 384);
    }

    #[test]
    fn test_embed_empty_string() {
        let result = embed_text("");
        assert!(result.is_err());
    }
}
```

## Performance Considerations
- Use `cargo bench` for performance-critical code
- Profile before optimizing
- Document performance characteristics in PRs
- Run benchmarks before/after for comparison

## Documentation Changes
- Update relevant `.md` files
- Keep README.md up to date
- Add examples for new features
- Update CHANGELOG.md

## Getting Help

- **Questions**: Open a GitHub Discussion
- **Bugs**: Create a bug report issue
- **Chat**: Join our Discord/Slack (if available)
- **Email**: * **Saketha Rama:** [sakethram9999@gmail.com](mailto:sakethram9999@gmail.com),  **Avinash Changrani:** [another@email.com](mailto:avinashchangrani99@email.com)

## Recognition

Contributors are recognized in:
- GitHub contributors page
- Release notes
- CHANGELOG.md

## Code of Conduct

This project adheres to the [Contributor Covenant Code of Conduct](CODE_OF_CONDUCT.md).
By participating, you are expected to uphold this code.

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

**Happy Contributing! **
