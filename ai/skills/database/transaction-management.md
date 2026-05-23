# Transaction Management Standards

## Objective

Define enterprise-grade transaction management standards for all J4MB backend services.

Transactions must ensure:
- consistency
- integrity
- auditability
- retry safety
- tenant isolation

---

# Transaction Philosophy

Transactions protect business invariants.

Transactions must:
- remain explicit
- remain bounded
- remain observable

Avoid:
- hidden transactional behavior
- long-running transactions
- distributed transaction assumptions

---

# Transaction Boundary Standards

Transactions belong in:
- application/service layer

Avoid:
- transactions in controllers
- transactions in presentation layer

---

# Transaction Scope Standards

Transactions should:
- remain small
- remain focused
- protect a single consistency boundary

Avoid:
- excessively broad transactional workflows

---

# ACID Standards

Critical financial workflows must preserve:
- atomicity
- consistency
- isolation
- durability

Examples:
- ledger posting
- payment processing
- balance updates

---

# Retry Safety Standards

Transactions must support:
- safe retries
- idempotent operations
- duplicate protection

Critical for:
- Kafka consumers
- distributed workflows
- external retries

---

# Distributed System Standards

Avoid:
- distributed ACID assumptions

Preferred:
- eventual consistency
- outbox pattern
- compensating workflows

---

# Financial Transaction Standards

Financial operations must:
- remain immutable
- remain traceable
- remain audit-safe

Never:
- partially commit financial operations

---

# Tenant Isolation Standards

Transactions must:
- remain tenant-scoped
- preserve schema isolation

Never:
- mix tenant operations in same transaction

---

# Exception Handling Standards

Transactional failures must:
- rollback safely
- remain observable
- preserve consistency

Avoid:
- swallowed exceptions
- hidden rollback behavior

---

# Isolation Level Standards

Use default isolation unless:
- business correctness requires stronger guarantees

Avoid:
- unnecessary pessimistic locking

---

# Async Workflow Standards

Async processing must support:
- retry safety
- duplicate prevention
- eventual consistency

Avoid:
- assuming exactly-once delivery

---

# Outbox Pattern Standards

Event publication should support:
- transactional consistency
- reliable delivery
- replay safety

Preferred:
- outbox pattern for Kafka integration

---

# Long-Running Workflow Standards

Long-running workflows should use:
- saga orchestration
- compensating actions

Avoid:
- long database transactions

---

# Observability Standards

Transactions should support:
- traceability
- correlation IDs
- tenant-aware logging

Failures must remain:
- diagnosable
- traceable

---

# AI Code Generation Rules

AI-generated transactional code must:
- preserve consistency
- avoid hidden side effects
- support retry safety
- avoid broad transaction scopes

Do not generate:
- transaction leakage
- controller transactions
- unsafe distributed assumptions
- partial financial updates

---

# Long-Term Principles

Transactional correctness is foundational for:
- fintech
- SaaS
- event-driven systems
- distributed systems

Correctness is more important than convenience.
