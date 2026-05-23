# Financial System Standards

## Objective

Define enterprise-grade financial system standards for all J4MB fintech and ledger services.

Financial systems must prioritize:
- correctness
- consistency
- immutability
- auditability
- transactional safety

---

# Financial System Philosophy

Financial correctness is non-negotiable.

Systems must prioritize:
- consistency over convenience
- correctness over performance shortcuts
- auditability over hidden optimization

---

# Monetary Standards

Always use:
- BigDecimal in Java
- NUMERIC(p,s) in PostgreSQL

Never use:
- float
- double

---

# Currency Standards

All monetary operations must:
- validate currency consistency
- store ISO currency codes

Avoid:
- implicit currency assumptions

---

# Ledger Standards

Ledger systems must support:
- double-entry accounting
- immutable journal entries
- balanced transactions

Invariant:
debit == credit

must NEVER break.

---

# Immutability Standards

Financial history must remain:
- append-only
- immutable
- traceable

Avoid:
- destructive financial updates
- overwriting transaction history

---

# Transaction Standards

Financial operations must:
- remain ACID-compliant
- rollback safely
- support retry safety

Avoid:
- partial financial commits

---

# Idempotency Standards

Critical financial workflows must support:
- retry safety
- duplicate prevention

Examples:
- payment processing
- ledger posting
- transfers

---

# Auditability Standards

All financial operations must record:
- timestamps
- user identity
- tenant identity
- trace IDs
- transaction references

---

# Multi-Tenant Standards

Financial isolation must remain:
- tenant-safe
- schema-isolated
- audit-safe

Never:
- mix tenant financial state

---

# Concurrency Standards

Financial systems must protect against:
- race conditions
- duplicate processing
- inconsistent balances

Use:
- optimistic locking where appropriate

---

# Balance Calculation Standards

Balances should preferably derive from:
- journal history
- immutable transaction records

Avoid:
- hidden balance mutation logic

---

# External Payment Standards

External payment integrations must support:
- retries
- reconciliation
- idempotency
- traceability

---

# Reconciliation Standards

Systems should support:
- reconciliation workflows
- mismatch detection
- audit investigation

---

# Security Standards

Financial systems require:
- strict authorization
- tenant isolation
- secure audit trails

Never expose:
- sensitive financial data improperly

---

# Observability Standards

Financial workflows must support:
- detailed tracing
- structured logging
- operational diagnostics

---

# AI Code Generation Rules

AI-generated financial code must:
- preserve correctness
- support auditability
- support idempotency
- avoid floating-point arithmetic
- preserve immutable history

Do not generate:
- unsafe money calculations
- mutable ledger history
- duplicate-prone workflows
- hidden balance mutations

---

# Long-Term Principles

Financial systems require:
- operational trust
- deterministic behavior
- strong consistency
- explainable history

Correctness is always the highest priority.
