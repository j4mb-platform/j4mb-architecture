# Logging Standards

## Objective

Define enterprise-grade logging standards for all backend services.

Logging must support:
- observability
- debugging
- incident response
- distributed tracing
- operational diagnostics
- auditability

Logs are operational assets.

---

# Logging Philosophy

Logging must:
- provide operational value
- support traceability
- remain structured
- remain consistent

Logs should help answer:
- what happened
- when it happened
- where it happened
- why it failed
- which tenant/user was impacted

Avoid:
- noisy logging
- meaningless logs
- duplicated logs
- sensitive data leakage

---

# Logging Framework Standards

Use:
- SLF4J
- Logback

Preferred:
- structured JSON logging

Avoid:
- System.out.println
- inconsistent logging frameworks

---

# Structured Logging Standards

Logs must remain structured.

Preferred fields:
- timestamp
- level
- service
- traceId
- correlationId
- tenantId
- userId
- thread
- logger
- message

Example:

```json
{
  "timestamp": "2026-05-23T12:00:00Z",
  "level": "INFO",
  "service": "j4mb-ledger",
  "traceId": "abc123",
  "tenantId": "tenant-1",
  "message": "Account created successfully"
}
```

---

# Log Level Standards

Use proper log levels consistently.

---

# ERROR

Use for:
- failed operations
- unexpected exceptions
- infrastructure failures
- data consistency risks

Examples:
- database connection failure
- Kafka publish failure
- payment processing failure

ERROR logs must:
- include traceability context
- support operational diagnosis

---

# WARN

Use for:
- recoverable issues
- unexpected but non-fatal situations
- fallback activation

Examples:
- retry triggered
- invalid optional payload
- degraded external service

Avoid excessive WARN usage.

---

# INFO

Use for:
- important business operations
- startup lifecycle events
- significant workflow transitions

Examples:
- application started
- payment processed
- tenant provisioned

INFO logs should remain meaningful.

Avoid:
- excessive operational noise

---

# DEBUG

Use for:
- detailed development diagnostics
- troubleshooting support

DEBUG logs may include:
- workflow progression
- query details
- intermediate states

Avoid enabling DEBUG heavily in production.

---

# TRACE

Use only for:
- deep troubleshooting
- framework-level diagnostics

TRACE should rarely be enabled.

---

# Correlation ID Standards

All requests must support:
- correlation IDs
- trace propagation

Correlation IDs must:
- flow across services
- flow across async messaging
- remain searchable

Required for:
- distributed tracing
- incident debugging

---

# Tenant-Aware Logging

Multi-tenant systems must include:
- tenantId
- tenant context

Requirements:
- tenant traceability
- tenant-safe diagnostics

Never:
- leak cross-tenant information

---

# Security Logging Standards

Security-sensitive operations must be logged.

Examples:
- login attempts
- failed authentication
- permission denials
- token validation failures

Never log:
- passwords
- JWT tokens
- secrets
- API keys
- sensitive personal data

---

# Financial Logging Standards

Financial operations require audit-grade logging.

Examples:
- journal entry creation
- payment processing
- balance updates
- transaction reversals

Requirements:
- traceability
- consistency
- idempotency diagnostics

Avoid:
- incomplete financial logs

---

# Exception Logging Standards

Exceptions must:
- include context
- include trace IDs
- support debugging

Avoid:
- duplicate stack trace logging
- swallowed exceptions

Never:
- log and rethrow repeatedly across layers

---

# API Logging Standards

Log:
- incoming requests
- response status
- execution duration
- request trace IDs

Avoid logging:
- full request bodies containing sensitive data
- credentials
- personal sensitive information

---

# Performance Logging Standards

Log performance metrics for:
- slow queries
- long-running requests
- external integrations
- Kafka processing delays

Threshold-based logging preferred.

Example:
- requests exceeding 2 seconds

---

# Database Logging Standards

Log:
- connectivity failures
- migration execution
- transaction failures

Avoid:
- excessive SQL logging in production

Sensitive query data must remain protected.

---

# Kafka Logging Standards

Kafka workflows must log:
- publish failures
- consumer retries
- dead-letter events
- message processing failures

Logs must support:
- replay diagnostics
- event tracing
- distributed debugging

---

# Startup Logging Standards

Applications should log:
- startup completion
- active profiles
- service version
- environment summary

Avoid:
- dumping full configurations
- exposing secrets

---

# Health Check Logging Standards

Avoid noisy health-check logging.

Do not flood logs with:
- frequent successful probes

Only log:
- health degradation
- dependency failures
- recovery events

---

# Observability Integration Standards

Logging must integrate with:
- OpenTelemetry
- Prometheus
- Grafana
- centralized log aggregation

Preferred:
- ELK Stack
- Loki
- OpenSearch

---

# Log Retention Standards

Logs should support:
- operational retention
- audit requirements
- compliance needs

Retention policies should consider:
- storage cost
- legal requirements
- security requirements

---

# Async Logging Standards

Async processing must:
- preserve trace IDs
- preserve tenant context
- preserve correlation IDs

Critical for:
- Kafka consumers
- event-driven workflows
- background processing

---

# AI Code Generation Rules

AI-generated logging must:
- use structured logs
- include operational context
- support traceability
- avoid sensitive leakage

Do not generate:
- noisy logs
- meaningless logs
- duplicate logs
- secret exposure
- excessive debug logging

---

# Long-Term Operational Principles

Good logging enables:
- faster incident response
- distributed debugging
- production observability
- operational confidence
- platform reliability

Poor logging increases:
- downtime
- debugging time
- operational complexity
- support costs
