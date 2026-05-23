# Auditability Standards

## Objective

Define enterprise-grade auditability standards for all J4MB backend services.

Auditability must ensure:
- traceability
- accountability
- compliance readiness
- financial integrity
- operational visibility

---

# Audit Philosophy

Critical systems must explain:
- what happened
- when it happened
- who performed it
- why it changed

Auditability is mandatory for:
- fintech
- SaaS
- enterprise systems

---

# Audit Field Standards

All business entities should support:
- created_at
- created_by
- updated_at
- updated_by

Optional:
- deleted_at

---

# Immutable Financial History Standards

Financial records must remain:
- append-oriented
- immutable
- traceable

Never:
- overwrite transactional history

---

# User Traceability Standards

Critical operations must record:
- user identity
- tenant identity
- correlation IDs
- timestamps

---

# Multi-Tenant Audit Standards

Audit trails must remain:
- tenant-isolated
- schema-aware

Avoid:
- cross-tenant audit leakage

---

# Change Tracking Standards

Critical changes should support:
- before/after tracking
- change attribution
- historical reconstruction

---

# Event Audit Standards

Critical events should record:
- eventId
- tenantId
- traceId
- actor identity

---

# Security Audit Standards

Audit:
- login attempts
- permission failures
- role changes
- token failures

Never log:
- passwords
- secrets
- sensitive credentials

---

# Operational Audit Standards

Audit:
- migrations
- tenant provisioning
- schema changes
- deployment events

---

# Observability Standards

Audit trails must support:
- debugging
- incident response
- compliance investigations

---

# AI Code Generation Rules

AI-generated systems must:
- preserve audit history
- avoid destructive mutation
- support traceability
- record critical operations

Do not generate:
- silent destructive updates
- hidden financial mutations
- missing audit metadata

---

# Long-Term Principles

Auditability protects:
- trust
- compliance
- operational confidence
- financial correctness

Enterprise systems require explainable history.
