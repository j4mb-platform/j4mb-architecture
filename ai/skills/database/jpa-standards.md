# JPA Standards

## Objective

Define enterprise-grade JPA and Hibernate standards for all J4MB backend services.

Persistence architecture must prioritize:
- transactional correctness
- maintainability
- performance
- tenant isolation
- predictable behavior

---

# Persistence Philosophy

JPA is a persistence tool.

Business logic must NOT depend on:
- Hibernate internals
- persistence side effects
- lazy-loading assumptions

Persistence must remain:
- explicit
- observable
- predictable

---

# ORM Standards

Preferred:
- Spring Data JPA
- Hibernate

Requirements:
- explicit mappings
- tenant-safe persistence
- transaction awareness

Avoid:
- magic persistence behavior
- hidden lazy-loading side effects

---

# Entity Design Standards

Entities must:
- represent business concepts
- remain cohesive
- encapsulate invariants

Avoid:
- anemic entities
- public mutable state
- persistence-only modeling

---

# Entity Naming Standards

Use:
- singular nouns

Examples:
- Account
- JournalEntry
- Transaction

Avoid:
- AccountEntity
- Accounts

---

# Primary Key Standards

Preferred:
- UUID identifiers

Example:

```java
@Id
private UUID id;
```

Avoid:
- exposed sequential IDs

---

# Audit Field Standards

All entities should support:
- createdAt
- createdBy
- updatedAt
- updatedBy

Optional:
- deletedAt

---

# Lazy Loading Standards

Default:
- LAZY loading

Avoid:
- EAGER loading by default

EAGER loading frequently causes:
- performance degradation
- N+1 problems
- memory overhead

---

# Fetch Strategy Standards

Use:
- fetch joins
- entity graphs
- projection queries

Avoid:
- uncontrolled graph loading

---

# DTO Separation Standards

Never expose:
- JPA entities directly in APIs

Always separate:
- entities
- request DTOs
- response DTOs

---

# Transaction Boundary Standards

Transactions belong in:
- application/service layer

Avoid:
- transaction management in controllers
- transactional repositories only

---

# Cascade Standards

Use cascades carefully.

Allowed:
- aggregate ownership relationships

Avoid:
- broad CascadeType.ALL usage
- hidden persistence side effects

---

# Bidirectional Relationship Standards

Avoid unnecessary bidirectional relationships.

Prefer:
- unidirectional relationships where possible

Bidirectional mappings increase:
- complexity
- serialization risk
- maintenance overhead

---

# Equals & HashCode Standards

Avoid using:
- mutable fields

Preferred:
- identifier-based equality

---

# Multi-Tenant Standards

Persistence must support:
- schema-per-tenant isolation
- tenant-aware schema switching

Entities must remain:
- tenant-agnostic

Tenant isolation belongs in:
- infrastructure layer

---

# N+1 Prevention Standards

All repository queries must consider:
- fetch plans
- query optimization
- pagination

Avoid:
- accidental lazy loading loops

---

# Pagination Standards

Large datasets must use:
- pagination
- projections where appropriate

Avoid:
- loading large collections fully

---

# Repository Standards

Repositories should:
- focus on persistence concerns
- expose meaningful query methods

Avoid:
- business logic in repositories
- overly generic repositories

---

# Optimistic Locking Standards

Use:
- @Version where consistency matters

Critical for:
- financial systems
- concurrent updates
- distributed workflows

---

# Soft Delete Standards

Soft deletes should remain:
- explicit
- observable

Avoid:
- hidden global filters creating confusion

---

# Entity Lifecycle Standards

Avoid:
- excessive lifecycle callback complexity

Business workflows should remain:
- explicit in services

---

# Performance Standards

Monitor:
- query count
- execution time
- lazy loading behavior
- connection pool usage

Avoid:
- ORM abuse
- excessive abstraction

---

# Financial Persistence Standards

Financial entities should prioritize:
- immutability
- auditability
- append-oriented history

Avoid:
- mutating transactional history

---

# AI Code Generation Rules

AI-generated persistence code must:
- avoid EAGER loading abuse
- support tenant isolation
- separate DTOs from entities
- avoid N+1 issues
- preserve transactional correctness

Do not generate:
- generic base entities everywhere
- uncontrolled cascades
- entity exposure in APIs
- hidden lazy-loading problems

---

# Long-Term Principles

Persistence must remain:
- predictable
- observable
- maintainable
- scalable

ORM convenience must never override correctness.
