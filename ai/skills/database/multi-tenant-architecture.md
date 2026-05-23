# Multi-Tenant Architecture Standards

## Objective

Define enterprise-grade multi-tenant architecture standards for all J4MB platform services.

The platform uses:
- PostgreSQL
- schema-per-tenant isolation
- shared platform schema
- tenant-aware application context

The architecture must ensure:
- tenant isolation
- scalability
- operational manageability
- security
- SaaS readiness

---

# Multi-Tenant Philosophy

Tenant isolation is a security boundary.

The architecture must:
- prevent tenant data leakage
- support tenant scalability
- support operational isolation
- remain cloud-native ready

Multi-tenancy affects:
- persistence
- APIs
- logging
- caching
- messaging
- observability
- security
- migrations

---

# Multi-Tenant Strategy

Preferred strategy:
- schema-per-tenant

Example:

platform.tenants

tenant_acme.accounts
tenant_acme.transactions

tenant_nova.accounts
tenant_nova.transactions

---

# Architecture Overview

The platform is divided into:

1. Shared Platform Schema
2. Tenant Business Schemas

---

# Shared Platform Schema

The shared platform schema stores:
- tenant metadata
- user management
- subscriptions
- provisioning information
- platform-level configurations

Preferred schema:

platform

Example tables:
- platform.tenants
- platform.users
- platform.roles
- platform.subscriptions

---

# Tenant Schemas

Each tenant owns an isolated schema.

Examples:
- tenant_acme
- tenant_demo
- tenant_nova

Tenant schemas contain:
- accounts
- transactions
- journal_entries
- documents
- tasks
- notifications

---

# Tenant Isolation Principles

Tenant data must remain isolated at:
- schema level
- query level
- transaction level
- cache level
- event level
- logging level

Never:
- mix tenant schemas
- expose cross-tenant access
- share tenant persistence state

---

# Tenant Context Standards

All requests must resolve:
- tenantId
- tenantCode
- schemaName

Preferred object:

```java
public class TenantContext {
    private UUID tenantId;
    private String tenantCode;
    private String schemaName;
}
```

TenantContext must remain:
- request-scoped
- immutable where practical
- traceable

Never use:
- static global tenant state

---

# Tenant Resolution Standards

Tenant identity should be resolved using:
- JWT claims
- security context
- authenticated identity

Avoid:
- trusting raw client-provided tenant identifiers

Preferred flow:

JWT
↓
Authentication
↓
TenantResolver
↓
TenantContext
↓
Schema Resolution

---

# Hibernate Multi-Tenancy Standards

Preferred Hibernate strategy:

```java
MultiTenancyStrategy.SCHEMA
```

Required components:
- CurrentTenantIdentifierResolver
- MultiTenantConnectionProvider

The application must dynamically switch:
- PostgreSQL search_path
- tenant schema context

---

# PostgreSQL Schema Switching

Preferred approach:

```sql
SET search_path TO tenant_acme;
```

Requirements:
- schema reset after connection usage
- tenant-safe connection reuse
- transaction-safe schema switching

Avoid:
- leaking schema state across requests

---

# Tenant Provisioning Standards

Tenant onboarding must support:
- schema creation
- migration execution
- tenant metadata registration
- initial configuration

Tenant provisioning should eventually support:
- automation
- repeatability
- observability

Initially:
- manual provisioning is acceptable

Avoid:
- premature provisioning complexity

---

# Flyway Migration Standards

Migrations must support:
- tenant schema execution
- schema version consistency
- deterministic upgrades

Preferred approach:
- execute migrations per tenant schema

Migration example:

V1__create_accounts.sql
V2__create_transactions.sql

Requirements:
- immutable migrations
- version consistency
- rollback awareness

---

# Repository Standards

Repositories must remain:
- tenant-agnostic
- schema-aware indirectly

Business logic should NOT manually manage:
- schema switching
- tenant SQL routing

Tenant isolation should occur at:
- infrastructure layer

---

# Transaction Standards

Transactions must remain:
- tenant-isolated
- schema-safe
- traceable

Never:
- mix tenant operations in same transaction

---

# API Standards

APIs must:
- operate within authenticated tenant context
- avoid exposing schema details externally

Never expose:
- schema names
- internal tenant infrastructure

---

# Security Standards

Tenant isolation is a security requirement.

Requirements:
- tenant-aware authorization
- tenant-aware access validation
- secure tenant resolution

Never:
- trust tenant IDs from request payloads
- allow cross-tenant access paths

---

# Logging Standards

All logs must include:
- tenantId
- schemaName where appropriate
- correlationId
- traceId

This is critical for:
- debugging
- observability
- incident response

---

# Kafka/Event Standards

All events must include:
- tenantId
- correlationId
- traceId

Example:

```json
{
  "eventType": "AccountCreated",
  "tenantId": "tenant-acme",
  "traceId": "abc123"
}
```

This is critical for:
- distributed tracing
- replay safety
- tenant debugging

---

# Cache Standards

Caches must remain tenant-aware.

Cache keys should include:
- tenant identifiers

Example:

tenant_acme:account:123

Never:
- share tenant cache state accidentally

---

# Observability Standards

Metrics and traces should support:
- tenant-aware diagnostics
- schema-aware observability

Support:
- distributed tracing
- tenant-level monitoring

---

# Performance Standards

Requirements:
- connection pooling
- efficient schema switching
- indexed tenant metadata
- scalable migration execution

Avoid:
- excessive schema switching overhead
- schema leakage across pooled connections

---

# Backup & Restore Standards

The architecture should support:
- tenant-level backup
- tenant-level restore
- tenant migration
- tenant archival

Schema-per-tenant enables operational flexibility.

---

# Cross-Tenant Reporting Standards

Cross-tenant analytics should remain:
- explicit
- controlled
- platform-level only

Avoid:
- accidental tenant aggregation

Use:
- dedicated reporting workflows
- platform analytics pipelines

---

# Testing Standards

Testing must include:
- tenant isolation tests
- schema-switching tests
- cross-tenant leakage prevention
- migration consistency validation

Critical scenarios:
- concurrent tenants
- async workflows
- tenant provisioning

---

# AI Code Generation Rules

AI-generated code must:
- support schema-per-tenant architecture
- avoid tenant leakage
- preserve tenant context
- support tenant-aware logging
- support tenant-aware tracing

Do not generate:
- hardcoded schema names
- static tenant state
- unsafe tenant assumptions
- cross-tenant queries

---

# Long-Term Evolution

The architecture should support future:
- tenant sharding
- distributed databases
- tenant migration
- Kubernetes scaling
- event-driven workflows
- SaaS expansion

without major architectural rewrites.

# Keycloak Integration Standards

Preferred identity architecture:
- single Keycloak realm
- tenant-aware JWT claims
- schema-per-tenant persistence isolation

Tenant context should be resolved from:
- JWT claims
- authenticated security context

Preferred JWT claims:
- tenant_id
- tenant_code
- roles
- user_id

Example:

{
  "sub": "user-123",
  "tenant_id": "tenant-acme",
  "tenant_code": "acme",
  "roles": ["ACCOUNT_ADMIN"]
}

Avoid:
- realm-per-tenant architecture initially
- trusting tenant IDs from request payloads

Authorization must remain:
- tenant-aware
- role-aware
- security-context driven

Tenant schema resolution should derive from:
JWT
↓
Security Context
↓
TenantResolver
↓
TenantContext
↓
Schema Resolution

The persistence layer must never trust:
- client-provided schema names
- raw tenant identifiers

Future evolution may support:
- realm-per-tenant enterprise isolation
- external identity federation
- SSO integration
- tenant-specific identity providers
