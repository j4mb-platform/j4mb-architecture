# Database Design Standards

## Objective

Define enterprise-grade database design standards for all J4MB platform services.

Database architecture must prioritize:
- consistency
- auditability
- scalability
- tenant isolation
- maintainability
- operational safety

The platform uses:
- PostgreSQL
- schema-per-tenant isolation
- Flyway migrations
- transactional consistency
- future event-driven evolution

---

# Database Design Philosophy

Database design must start from:
1. business domains
2. business invariants
3. transactional boundaries
4. audit requirements
5. tenant isolation

Avoid designing databases from:
- CRUD thinking
- UI screens
- framework structures

The database is a business integrity layer.

---

# Core Design Principles

Databases must prioritize:
- correctness
- explicitness
- traceability
- operational clarity

Prefer:
- normalized schemas
- explicit constraints
- immutable financial records
- audit-friendly design

Avoid:
- premature denormalization
- hidden business logic
- uncontrolled schema evolution

---

# Database Technology Standards

Preferred database:
- PostgreSQL

Requirements:
- latest stable production-ready version
- ACID transactional guarantees
- schema support
- strong indexing capabilities

Avoid:
- unsupported databases
- inconsistent database technologies across services

---

# Multi-Tenant Architecture Standards

The platform uses:
- schema-per-tenant isolation

Architecture structure:

platform.tenants
platform.users

tenant_acme.accounts
tenant_acme.transactions

tenant_nova.accounts
tenant_nova.transactions

---

# Shared Platform Schema

The platform schema stores:
- tenant metadata
- provisioning information
- platform users
- subscriptions
- platform configurations

Preferred schema:
- platform

---

# Tenant Business Schemas

Each tenant owns:
- isolated schema
- isolated business tables
- isolated transactional data

Tenant schemas contain:
- accounts
- journal_entries
- transactions
- invoices
- documents
- tasks

---

# Schema Naming Standards

Use:
- lowercase
- snake_case
- tenant-prefixed schemas

Examples:
- tenant_acme
- tenant_demo

Avoid:
- spaces
- mixed casing
- special characters

---

# Table Design Standards

Tables must:
- represent business concepts
- remain cohesive
- support transactional consistency

Avoid:
- generic mega tables
- polymorphic persistence abuse
- unclear ownership

---

# Table Naming Standards

Use:
- plural snake_case names

Examples:
- accounts
- journal_entries
- payment_transactions

Avoid:
- camelCase tables
- inconsistent pluralization

---

# Column Naming Standards

Use:
- snake_case

Examples:
- created_at
- updated_at
- account_number
- journal_entry_id

Avoid:
- camelCase columns
- abbreviated unclear names

---

# Primary Key Standards

Preferred:
- UUID primary keys

Example:

```sql
id UUID PRIMARY KEY
```

Requirements:
- globally unique identifiers
- distributed-system compatibility

Avoid:
- sequential numeric IDs for exposed resources

---

# Foreign Key Standards

Foreign keys must:
- remain explicit
- enforce referential integrity

Examples:
- account_id
- transaction_id
- journal_entry_id

Never use:
- implicit relationships only

---

# Audit Field Standards

All business tables should include:

```sql
created_at TIMESTAMP NOT NULL,
created_by VARCHAR(255),
updated_at TIMESTAMP,
updated_by VARCHAR(255)
```

Optional:
```sql
deleted_at TIMESTAMP
```

Auditability is critical for:
- fintech
- SaaS
- enterprise systems

---

# Financial System Standards

Financial data must prioritize:
- immutability
- consistency
- traceability

Requirements:
- append-oriented transaction history
- immutable journal entries
- audit-safe operations

Never:
- silently mutate financial history
- overwrite transactional records

---

# Monetary Value Standards

Always use:
- NUMERIC(p,s)

Example:

```sql
amount NUMERIC(19,4)
```

Never use:
- FLOAT
- DOUBLE

Financial calculations require precision.

---

# Currency Standards

Currency-aware systems must:
- store ISO currency codes
- validate currency consistency

Example:

```sql
currency_code VARCHAR(3)
```

---

# Transactional Integrity Standards

Critical workflows must remain:
- ACID-compliant
- transaction-safe
- rollback-safe

Examples:
- ledger posting
- payment processing
- balance updates

---

# Indexing Standards

Indexes must support:
- tenant isolation
- transactional queries
- lookup performance

Index:
- foreign keys
- frequently queried fields
- unique business identifiers

Examples:

```sql
CREATE INDEX idx_accounts_number
ON accounts(account_number);
```

---

# Unique Constraint Standards

Business uniqueness must remain explicit.

Examples:

```sql
UNIQUE(account_number)
```

Multi-tenant uniqueness may require:
- schema-level isolation
or
- composite uniqueness

---

# Check Constraint Standards

Use explicit business constraints.

Examples:

```sql
CHECK(amount >= 0)
```

Constraints protect:
- business correctness
- data integrity

---

# JSON Column Standards

Use JSONB only when justified.

Allowed for:
- dynamic metadata
- extensible configuration
- event payload snapshots

Avoid:
- storing core business entities in JSON

---

# Soft Delete Standards

Use soft deletes carefully.

Preferred:
- immutable audit records
- archival strategies

Avoid:
- hidden filtering complexity
- accidental data resurrection

---

# Flyway Migration Standards

All schema changes must use:
- Flyway migrations

Migration naming:

V1__init.sql
V2__create_accounts.sql

Requirements:
- immutable migrations
- sequential ordering
- deterministic execution

Never:
- modify executed migrations

---

# Schema Evolution Standards

Database evolution must support:
- backward compatibility
- safe deployments
- incremental rollout

Avoid:
- destructive production changes
- unsafe column drops
- breaking migrations

---

# Query Standards

Queries must:
- remain explicit
- remain optimized
- avoid hidden side effects

Avoid:
- SELECT *
- N+1 query problems
- unbounded scans

---

# Pagination Standards

Large datasets must support:
- pagination
- filtering
- indexed sorting

Avoid:
- loading massive result sets into memory

---

# Performance Standards

Databases must support:
- connection pooling
- indexed access paths
- query optimization
- scalable tenant growth

Monitor:
- slow queries
- lock contention
- index usage

---

# Locking Standards

Use:
- optimistic locking by default

Use pessimistic locking only when:
- absolutely necessary
- transactional contention requires it

---

# Event-Driven Readiness

Database design should support future:
- Kafka integration
- outbox pattern
- event sourcing experiments
- distributed workflows

Avoid:
- tightly coupling schema to synchronous workflows only

---

# Security Standards

Databases must:
- protect tenant isolation
- avoid sensitive exposure
- support least privilege access

Never:
- expose direct production database access broadly
- store secrets in plaintext

---

# Backup & Recovery Standards

Architecture must support:
- tenant-level backup
- schema-level recovery
- disaster recovery
- migration rollback planning

---

# Testing Standards

Database testing must include:
- migration validation
- tenant isolation testing
- transactional consistency
- rollback testing

Use:
- Testcontainers

---

# AI Code Generation Rules

AI-generated database designs must:
- follow normalization principles
- support auditability
- support schema-per-tenant isolation
- use explicit constraints
- support Flyway migrations

Do not generate:
- weak financial schemas
- floating-point money fields
- hidden relationships
- unsafe destructive migrations
- tenant-unsafe structures

---

# Long-Term Architectural Principles

Database architecture should optimize for:
- long-term maintainability
- operational safety
- financial correctness
- tenant scalability
- distributed evolution

The database is a strategic architectural asset.
