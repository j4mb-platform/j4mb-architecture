# RBAC Authorization Standards

## Objective

Define role-based authorization standards for all J4MB services.

RBAC must support:
- tenant-aware permissions
- coarse-grained access control
- scalable enterprise authorization

---

# RBAC Philosophy

RBAC answers:
WHO can perform this action?

Roles should represent:
- business responsibilities
- operational capabilities

---

# Role Design Standards

Roles should remain:
- business-oriented
- stable
- coarse-grained

Examples:
- SYSTEM_ADMIN
- ACCOUNT_ADMIN
- ACCOUNTANT
- DOCUMENT_MANAGER

Avoid:
- excessive role explosion

---

# Tenant-Aware RBAC

Roles must remain:
- tenant-scoped
- isolated
- validated through authenticated context

Never:
- trust client-provided roles

---

# Permission Standards

Permissions should remain:
- explicit
- auditable
- centralized

Avoid:
- scattered hardcoded checks

---

# Spring Security Standards

Use:
- method security
- authorization annotations
- centralized access logic

---

# Audit Standards

Authorization decisions should support:
- auditability
- traceability
- tenant-aware logging

---

# AI Code Generation Rules

AI-generated authorization code must:
- validate roles
- preserve tenant isolation
- avoid hardcoded bypasses

Do not generate:
- unrestricted admin access
- implicit authorization
- weak role validation
