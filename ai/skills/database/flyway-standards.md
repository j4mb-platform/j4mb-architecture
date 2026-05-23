# Flyway Standards

## Objective

Define enterprise-grade Flyway migration standards for all J4MB platform services.

Database migrations must ensure:
- deterministic schema evolution
- tenant-safe upgrades
- operational consistency
- rollback awareness
- reproducible environments

---

# Migration Philosophy

Database schema is production infrastructure.

Schema evolution must:
- remain explicit
- remain versioned
- remain auditable
- remain reproducible

Never:
- modify databases manually in production
- rely on Hibernate auto-generation
- bypass migration governance

---

# Migration Tool Standards

Preferred:
- Flyway

Requirements:
- versioned migrations
- immutable migration history
- deterministic execution

Avoid:
- unmanaged schema changes
- mixed migration frameworks

---

# Migration Naming Standards

Use:

V1__init.sql
V2__create_accounts.sql
V3__add_journal_entries.sql

Requirements:
- sequential versioning
- descriptive naming
- immutable files

Avoid:
- vague names
- renamed migrations
- edited executed migrations

---

# Schema-Per-Tenant Standards

The platform uses:
- schema-per-tenant isolation

Flyway must support:
- tenant schema migrations
- schema version consistency
- isolated tenant upgrades

---

# Platform Schema Standards

Shared platform schema migrations:

platform.tenants
platform.users
platform.subscriptions

must remain separate from:
- tenant business schema migrations

---

# Tenant Migration Standards

Each tenant schema must:
- execute identical migration history
- remain version-consistent

Example:

tenant_acme → V15
tenant_nova → V15

Avoid:
- schema drift across tenants

---

# Migration Immutability

Executed migrations must NEVER be modified.

If changes are required:
- create new migration

Never:
- edit historical migrations
- rewrite migration history

---

# Rollback Philosophy

Flyway is forward-migration oriented.

Preferred strategy:
- corrective forward migrations

Avoid:
- destructive rollback assumptions

---

# Destructive Change Standards

Dangerous operations require:
- staged rollout
- data migration planning
- operational review

Examples:
- column drops
- table drops
- type changes

Prefer:
1. deprecate
2. migrate
3. remove later

---

# Tenant Provisioning Standards

New tenant onboarding must:
- create schema
- execute Flyway migrations
- validate schema consistency

Provisioning should remain:
- repeatable
- observable
- automated eventually

---

# Migration Execution Standards

Migrations must:
- execute automatically during startup where appropriate
- fail fast on inconsistencies

Avoid:
- partially applied migrations
- silent migration failures

---

# Transactional Migration Standards

Migrations should remain:
- transactional where supported
- atomic
- deterministic

Avoid:
- non-repeatable migration logic
- external side effects inside migrations

---

# Data Migration Standards

Data migrations must:
- remain explicit
- remain versioned
- support operational safety

Avoid:
- hidden data mutations
- manual production fixes

---

# Multi-Environment Standards

Migration behavior must remain consistent across:
- local
- dev
- staging
- production

Avoid:
- environment-specific schema drift

---

# Financial System Standards

Financial tables require:
- backward compatibility
- audit preservation
- immutable transactional history

Never:
- destructively rewrite financial history

---

# Observability Standards

Migration execution should log:
- migration version
- execution duration
- failures
- tenant schema context

Support:
- operational tracing
- deployment diagnostics

---

# AI Code Generation Rules

AI-generated migrations must:
- remain explicit
- support schema-per-tenant architecture
- preserve data integrity
- avoid destructive unsafe operations

Do not generate:
- ddl-auto usage
- unsafe drops
- mutable migration history
- tenant-unsafe migrations

---

# Long-Term Principles

Database migration history becomes:
- operational history
- deployment history
- infrastructure truth

Migration discipline is critical for enterprise systems.
