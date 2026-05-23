# Keycloak Integration Standards

## Objective

Define Keycloak integration standards for all J4MB services.

Keycloak architecture must support:
- centralized identity
- tenant-aware authentication
- RBAC
- future microservice scaling

---

# Identity Architecture

Preferred:
- single realm
- tenant-aware JWT claims
- schema-per-tenant persistence isolation

Avoid initially:
- realm-per-tenant complexity

---

# Required JWT Claims

Required claims:
- tenant_id
- tenant_code
- roles
- sub

---

# Role Mapping Standards

Roles should remain:
- business-oriented
- tenant-aware

Examples:
- ACCOUNT_ADMIN
- FINANCE_MANAGER
- DOCUMENT_APPROVER

Avoid:
- overly generic roles

---

# Service Authentication Standards

Microservices should use:
- OAuth2 Resource Server
- JWT validation

Service-to-service auth should support:
- machine accounts
- client credentials flow

---

# Tenant Resolution Flow

JWT
↓
Security Context
↓
TenantResolver
↓
TenantContext
↓
Schema Resolution

---

# Future Evolution

Architecture should support future:
- SSO
- external identity federation
- enterprise identity providers
- realm isolation if needed

---

# AI Code Generation Rules

AI-generated Keycloak integration must:
- preserve tenant isolation
- validate JWT claims
- support distributed auth

Do not generate:
- insecure trust assumptions
- hardcoded realm logic
- weak token validation
