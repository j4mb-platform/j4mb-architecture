# Idempotency Standards

## Objective

Define enterprise-grade idempotency standards for all J4MB backend services.

Idempotency must ensure:
- retry safety
- duplicate prevention
- financial correctness
- distributed consistency
- replay safety

---

# Idempotency Philosophy

Retries are inevitable.

Systems must guarantee:
same request → same result

especially for:
- financial operations
- Kafka consumers
- external callbacks
- distributed workflows

---

# API Idempotency Standards

Critical APIs must support:
- idempotency keys

Examples:
- payment processing
- ledger posting
- external callbacks

Preferred header:

Idempotency-Key

---

# Financial System Standards

Financial operations must NEVER:
- double charge
- duplicate transfer
- duplicate ledger posting

Financial correctness requires:
- idempotent processing
- immutable transaction references

---

# Database Deduplication Standards

Use:
- unique constraints
- operation tracking
- request identifiers

Example:
- unique transaction reference

---

# Kafka Idempotency Standards

Kafka consumers must support:
- replay safety
- duplicate detection
- retry safety

Avoid:
- assuming exactly-once delivery

Preferred:
- at-least-once + idempotency

---

# Event Processing Standards

Events should include:
- eventId
- traceId
- tenantId

Consumers must track:
- processed events
- duplicate prevention

---

# Retry Standards

Retries must remain:
- safe
- deterministic
- observable

Avoid:
- unsafe repeated side effects

---

# Async Workflow Standards

Async workflows must support:
- replay safety
- duplicate suppression
- dead-letter handling

---

# Transaction Standards

Idempotency and transactions must work together.

Critical workflows require:
- transactional deduplication
- atomic state changes

---

# Multi-Tenant Standards

Idempotency tracking must remain:
- tenant-aware
- schema-isolated

Avoid:
- cross-tenant deduplication leakage

---

# API Response Standards

Repeated identical requests should:
- return consistent responses
- avoid duplicate side effects

---

# Observability Standards

Idempotent workflows should log:
- duplicate detection
- replay handling
- retry attempts

Support:
- traceability
- debugging

---

# AI Code Generation Rules

AI-generated workflows must:
- support retry safety
- prevent duplicate operations
- preserve financial correctness
- support event replay safety

Do not generate:
- duplicate-prone financial workflows
- unsafe retries
- non-deterministic side effects

---

# Long-Term Principles

Distributed systems require:
- retry tolerance
- replay safety
- duplicate resistance

Idempotency is foundational for reliable enterprise systems.
