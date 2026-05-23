# Secrets Management Standards

## Objective

Define secrets management standards for all J4MB services.

Secrets management must ensure:
- secure credential handling
- environment isolation
- operational safety

---

# Secret Management Philosophy

Secrets must NEVER exist in:
- source code
- Git repositories
- Docker images

---

# Secret Categories

Examples:
- database passwords
- JWT secrets
- API keys
- certificates
- encryption keys

---

# Storage Standards

Use:
- environment variables
- secret management systems
- Kubernetes secrets later

Avoid:
- plaintext configuration files

---

# Rotation Standards

Secrets should support:
- rotation
- expiration
- revocation

---

# Logging Standards

Never log:
- passwords
- tokens
- secrets
- certificates

---

# Local Development Standards

Use:
- .env
- local overrides

Never commit:
- local secrets
- production credentials

---

# CI/CD Standards

Pipelines must:
- inject secrets securely
- avoid secret exposure in logs

---

# AI Code Generation Rules

AI-generated code must:
- externalize secrets
- avoid hardcoded credentials
- support secure configuration

Do not generate:
- embedded secrets
- plaintext credentials
- unsafe secret handling
