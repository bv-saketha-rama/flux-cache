# Security Policy

## Our Commitment

FluxCache is designed for **production LLM applications** handling sensitive data (customer queries, API responses, embeddings). Security is paramount to our mission of providing enterprise-grade semantic caching.

As we work toward production-readiness (v1.0), we take all security vulnerabilities seriously and appreciate responsible disclosure.

## Supported Versions

Currently, we support the following versions with security updates:

| Version | Supported          |
| ------- | ------------------ |
| 0.1.x   | :white_check_mark: |
| < 0.1   | :x:                |

## Reporting a Vulnerability

**Please do not report security vulnerabilities through public GitHub issues.**

Instead, please report them via email to 
* **Saketha Rama:** [sakethram9999@gmail.com](mailto:sakethram9999@gmail.com)
* **Avinash Changrani:** [another@email.com](mailto:avinashchangrani99@email.com)

Include the following information:
- Type of vulnerability
- Full paths of source file(s) related to the vulnerability
- Location of the affected source code (tag/branch/commit or direct URL)
- Step-by-step instructions to reproduce the issue
- Proof-of-concept or exploit code (if possible)
- Impact of the issue

## Response Timeline

- **Initial Response**: Within 48 hours
- **Status Update**: Within 7 days
- **Fix Timeline**: Depends on severity, typically 14-30 days

## Disclosure Policy

- Security issues are addressed privately
- We will notify you when the issue is fixed
- We will publish a security advisory after the fix is released
- Credit will be given to reporters (unless you prefer to remain anonymous)

## Security Best Practices

When deploying FluxCache in production:

### Data Protection
- **PII Handling**: Be cautious caching responses containing Personally Identifiable Information
- **Encryption**: Use TLS for Redis connections in production (`rediss://` protocol)
- **Cache TTL**: Set appropriate expiration times to limit data retention
- **Data Isolation**: Use separate Redis instances/databases for different tenants

### Access Control
- **Redis Authentication**: Always enable Redis authentication (`requirepass`)
- **Network Security**: Restrict Redis access via firewall rules
- **API Keys**: Use environment variables for LLM provider API keys
- **Never commit** `.env` files or credentials to version control

### Operational Security
- **Dependency Updates**: Keep Rust dependencies and Redis up to date
- **Rate Limiting**: Implement rate limits to prevent cache poisoning attacks
- **Audit Logging**: Enable logging for cache hits/misses in production
- **Monitoring**: Use Prometheus metrics to detect anomalies

### Development
- **Code Review**: All PRs require security review for sensitive areas
- **Input Validation**: Sanitize all user inputs before embedding/caching
- **Error Handling**: Don't leak sensitive information in error messages

## Bug Bounty

We currently do not offer a bug bounty program, but we deeply appreciate
security research and will acknowledge all valid reports.
