# JWT Authentication Standards

## Objective

Define JWT authentication standards for all J4MB services.

JWT architecture must support:
- stateless authentication
- tenant-aware identity
- distributed systems
- microservice propagation

---

# JWT Standards

Preferred:
- signed JWT tokens
- short-lived access tokens
- secure refresh flows

Identity provider:
- Keycloak

---

# Required Claims

JWTs should include:
- sub
- tenant_id
- tenant_code
- roles
- email
- preferred_username

Example:

{
  "sub": "user-123",
  "tenant_id": "tenant-acme",
  "roles": ["ACCOUNT_ADMIN"]
}

---

# Token Validation Standards

Services must validate:
- signature
- expiration
- issuer
- audience

Never trust:
- unsigned tokens
- malformed claims

---

# Multi-Tenant Standards

Tenant context derives from:
- validated JWT claims

Never:
- trust tenant IDs from requests

---

# Token Lifetime Standards

Access tokens:
- short-lived

Refresh tokens:
- securely managed

Avoid:
- long-lived insecure tokens

---

# Service Propagation Standards

JWT propagation must support:
- microservices
- Kafka tracing
- distributed workflows

---

# AI Code Generation Rules

AI-generated authentication code must:
- validate tokens properly
- preserve tenant isolation
- support secure token handling

Do not generate:
- insecure token parsing
- disabled validation
- hardcoded JWT secrets
