# Security Standards

## Objective

Define enterprise-grade security standards for all J4MB platform services.

Security must ensure:
- tenant isolation
- authentication
- authorization
- traceability
- least privilege access
- secure distributed communication

---

# Security Philosophy

Security is a core architecture concern.

Security must be:
- centralized
- explicit
- observable
- defense-in-depth oriented

Avoid:
- implicit trust
- hidden authorization logic
- security-by-obscurity

---

# Zero Trust Principles

Never trust:
- client input
- frontend validation
- internal network assumptions
- external integrations automatically

Always validate:
- identity
- permissions
- tenant ownership
- resource access

---

# Authentication Standards

Preferred:
- OAuth2
- OpenID Connect
- JWT-based authentication

Identity provider:
- Keycloak

Avoid:
- session-based scaling assumptions
- custom authentication systems

---

# Authorization Standards

Use:
- RBAC + ABAC hybrid model

RBAC:
- coarse-grained permissions

ABAC:
- contextual fine-grained access

---

# Multi-Tenant Security Standards

Tenant isolation is a security boundary.

Requirements:
- tenant-aware authorization
- tenant-safe logging
- tenant-safe persistence
- schema isolation

Never:
- trust tenant IDs from request payloads

---

# API Security Standards

APIs must:
- require authentication
- validate authorization
- support traceability
- enforce tenant boundaries

Never expose:
- internal endpoints publicly
- administrative operations unintentionally

---

# Secret Management Standards

Never hardcode:
- passwords
- JWT secrets
- API keys
- certificates

Use:
- environment variables
- secret management systems

---

# Logging & Audit Standards

Security operations must log:
- authentication attempts
- authorization failures
- tenant violations
- token failures

Never log:
- passwords
- secrets
- tokens

---

# AI Code Generation Rules

AI-generated code must:
- validate authorization
- preserve tenant isolation
- avoid insecure defaults
- support traceability

Do not generate:
- disabled security
- hardcoded secrets
- unrestricted endpoints
- trust-based authorization
