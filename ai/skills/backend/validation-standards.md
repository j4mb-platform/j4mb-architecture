# Validation Standards

## Objective

Define enterprise-grade validation standards for all backend services.

Validation must ensure:
- data integrity
- business correctness
- security enforcement
- tenant isolation
- domain consistency

Validation applies to:
- APIs
- domain logic
- persistence operations
- async events
- external integrations

---

# Validation Philosophy

Validation is multi-layered.

Validation must occur at:
1. API boundaries
2. application workflows
3. domain invariants
4. persistence constraints
5. distributed integration boundaries

Never rely on:
- frontend validation only
- database constraints only

---

# Validation Categories

## Structural Validation

Ensures:
- required fields exist
- formats are valid
- request structures are correct

Examples:
- null checks
- string length
- email format
- UUID format

---

## Business Validation

Ensures:
- business rules remain valid
- workflows remain consistent

Examples:
- account balance cannot go negative
- journal entries must balance
- payment amount must be positive

---

## Security Validation

Ensures:
- user authorization
- tenant ownership
- access restrictions

Examples:
- tenant access validation
- resource ownership checks
- RBAC enforcement

---

## Persistence Validation

Ensures:
- uniqueness
- referential integrity
- transactional consistency

Examples:
- duplicate account prevention
- foreign key consistency
- optimistic locking

---

# API Validation Standards

Use:
- Jakarta Validation

Required annotations:
- @NotNull
- @NotBlank
- @Size
- @Email
- @Pattern
- @Positive
- @PositiveOrZero

All request DTOs must be validated.

Example:

```java
public record CreateAccountRequest(
    @NotBlank String accountName,
    @NotNull UUID tenantId
) {}
```

---

# Controller Validation Standards

Use:
- @Valid
- @Validated

Example:

```java
@PostMapping
public ResponseEntity<AccountResponse> create(
    @Valid @RequestBody CreateAccountRequest request
)
```

Controllers must:
- validate requests
- reject invalid payloads early

Controllers must NOT:
- contain business validation logic

---

# Centralized Validation Handling

Validation failures must be handled centrally.

Use:
- @RestControllerAdvice

Requirements:
- standardized error responses
- field-level validation details
- traceable failures

Example response:

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation failed",
    "details": [
      {
        "field": "accountName",
        "message": "must not be blank"
      }
    ]
  }
}
```

---

# Domain Validation Standards

Business invariants belong inside the domain layer.

Examples:
- journal entries must balance
- transaction amounts must remain positive
- tenant ownership must remain consistent

Domain validation must:
- protect business correctness
- remain framework-independent

Avoid:
- placing business invariants only in controllers

---

# Financial Validation Standards

Critical for ledger and payment systems.

Requirements:
- exact decimal handling
- currency consistency
- transactional validation
- idempotency support

Use:
- BigDecimal for money

Never use:
- float
- double

Financial operations must validate:
- positive amounts
- balance consistency
- debit/credit equality
- currency compatibility

---

# Multi-Tenant Validation Standards

All tenant-aware operations must validate:
- tenant ownership
- tenant isolation
- tenant context consistency

Requirements:
- tenant context propagation
- tenant-aware resource validation

Never:
- trust raw tenant IDs from clients
- expose cross-tenant resources

---

# Security Validation Standards

Security validation must include:
- authentication checks
- authorization checks
- role validation
- ownership validation

Never trust:
- client-provided permissions
- client-provided roles

---

# Persistence Validation Standards

Database constraints must complement application validation.

Use:
- unique constraints
- foreign keys
- indexes
- check constraints

Avoid:
- relying solely on database failures

---

# Event Validation Standards

Incoming events must validate:
- schema compatibility
- tenant ownership
- business correctness
- idempotency

Invalid events must:
- fail safely
- support observability
- avoid corrupting workflows

---

# File Upload Validation Standards

Uploaded files must validate:
- file size
- content type
- extension consistency
- malware scanning where applicable

Never trust:
- file extensions alone

---

# Input Sanitization Standards

Sanitize:
- user input
- external payloads
- query parameters

Protect against:
- SQL injection
- XSS
- path traversal
- malformed payload attacks

---

# Validation Error Standards

Validation errors must:
- remain structured
- remain human-readable
- support debugging

Avoid:
- exposing internal stack traces
- leaking sensitive information

---

# Async Workflow Validation

Async workflows must validate:
- message integrity
- duplicate processing
- replay safety
- tenant ownership

Support:
- idempotent processing
- dead-letter handling

---

# Null Handling Standards

Avoid null-heavy designs.

Prefer:
- Optional where appropriate
- explicit validation
- defensive programming

Never:
- silently ignore null issues

---

# AI Code Generation Rules

AI-generated code must:
- validate all external input
- enforce business invariants
- use proper validation annotations
- generate centralized validation handling

Do not generate:
- unvalidated APIs
- weak financial validation
- missing tenant validation
- insecure input handling

---

# Long-Term Validation Principles

Validation protects:
- system correctness
- financial integrity
- tenant isolation
- operational stability

Validation failures should occur:
- early
- explicitly
- predictably
- safely
