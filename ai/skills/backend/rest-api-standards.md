# REST API Standards

## Objective

Define enterprise-grade REST API standards for all J4MB backend services.

These standards ensure:
- consistency
- predictability
- scalability
- client compatibility
- integration stability
- long-term maintainability

---

# API Design Principles

APIs must be:
- resource-oriented
- versioned
- predictable
- self-descriptive
- stateless

APIs are long-term contracts.

Avoid breaking changes whenever possible.

---

# REST Resource Naming

Use:
- plural nouns
- lowercase paths
- hyphen-separated names when needed

Examples:
- /api/v1/accounts
- /api/v1/payments
- /api/v1/journal-entries

Avoid:
- verbs in endpoints
- mixed naming conventions

Avoid:
- /getAccounts
- /createPayment
- /accountService

---

# API Versioning

All APIs must be versioned.

Preferred:
- URI versioning

Examples:
- /api/v1/accounts
- /api/v2/payments

Avoid:
- unversioned production APIs

---

# HTTP Method Standards

Use proper HTTP semantics.

## GET
Retrieve resources.

Must:
- remain idempotent
- avoid state changes

---

## POST
Create resources or trigger non-idempotent operations.

Examples:
- create account
- process payment

---

## PUT
Replace entire resources.

Must:
- remain idempotent

---

## PATCH
Partially update resources.

Use for:
- status updates
- partial modifications

---

## DELETE
Remove resources.

Must:
- remain idempotent where possible

---

# Response Format Standards

All responses must follow standardized structures.

---

# Success Response Format

```json
{
  "success": true,
  "data": {},
  "timestamp": "2026-05-23T12:00:00Z"
}
```

---

# Error Response Format

```json
{
  "success": false,
  "error": {
    "code": "ACCOUNT_NOT_FOUND",
    "message": "Account not found",
    "details": []
  },
  "timestamp": "2026-05-23T12:00:00Z",
  "traceId": "abc123"
}
```

---

# Response Principles

Responses must:
- remain consistent
- include timestamps
- support traceability
- avoid framework leakage

Never expose:
- stack traces
- internal exceptions
- database errors

---

# HTTP Status Code Standards

Use meaningful status codes.

---

## 200 OK
Successful retrieval or update.

---

## 201 Created
Successful resource creation.

---

## 204 No Content
Successful operation without response body.

---

## 400 Bad Request
Validation or malformed request failures.

---

## 401 Unauthorized
Authentication required.

---

## 403 Forbidden
Access denied.

---

## 404 Not Found
Resource not found.

---

## 409 Conflict
Business conflicts or duplicate resources.

---

## 422 Unprocessable Entity
Business rule validation failures.

---

## 500 Internal Server Error
Unexpected server failures.

Avoid returning:
- generic 200 for failures
- incorrect status semantics

---

# Request Validation Standards

All incoming requests must be validated.

Use:
- Jakarta Validation

Examples:
- @NotNull
- @NotBlank
- @Email
- @Size

Validation failures must return:
- structured error responses
- meaningful messages

---

# Pagination Standards

All list endpoints must support pagination.

Preferred query parameters:

?page=0&size=20&sort=createdAt,desc

Response example:

```json
{
  "success": true,
  "data": [],
  "pagination": {
    "page": 0,
    "size": 20,
    "totalElements": 120,
    "totalPages": 6
  }
}
```

Avoid:
- unbounded large result sets

---

# Filtering Standards

Filtering must:
- remain explicit
- support composability
- remain predictable

Examples:
- ?status=ACTIVE
- ?tenantId=tenant-1

Avoid:
- hidden filtering behavior

---

# Sorting Standards

Support explicit sorting.

Examples:
- ?sort=createdAt,desc
- ?sort=accountName,asc

Avoid:
- inconsistent sorting formats

---

# Idempotency Standards

Critical operations should support idempotency where appropriate.

Examples:
- payment processing
- transaction submission

Use:
- idempotency keys
- request tracking

Avoid:
- duplicate financial operations

---

# Multi-Tenant API Standards

APIs must support tenant isolation.

Tenant context may be resolved using:
- JWT claims
- headers
- security context

Never:
- trust tenant identifiers directly from clients without validation

---

# Security Standards

APIs must:
- require authentication where appropriate
- enforce authorization
- validate ownership and tenant access

Never expose:
- internal admin endpoints publicly
- sensitive information in responses

---

# DTO Standards

Always separate:
- request DTOs
- response DTOs
- internal entities

Never expose:
- JPA entities directly

---

# Error Handling Standards

Use centralized exception handling.

Requirements:
- business-specific error codes
- consistent error structures
- trace IDs
- meaningful messages

Avoid:
- raw exceptions
- inconsistent error payloads

---

# Logging Standards

APIs must support:
- request tracing
- correlation IDs
- tenant-aware logging

Never log:
- passwords
- tokens
- sensitive personal data

---

# OpenAPI Standards

All APIs must generate:
- OpenAPI documentation
- Swagger UI

Documentation must include:
- endpoint descriptions
- request examples
- response examples
- error responses

---

# Performance Standards

APIs should:
- support pagination
- avoid N+1 queries
- optimize serialization
- avoid excessive payload sizes

Avoid:
- returning massive nested objects
- unnecessary eager loading

---

# Async API Considerations

Long-running operations should support:
- asynchronous processing
- polling
- event-driven completion

Examples:
- document processing
- bulk imports
- report generation

---

# File Upload Standards

File uploads must:
- validate content type
- validate size
- support secure storage
- avoid direct filesystem persistence

Preferred:
- object storage integration

---

# API Evolution Principles

Prefer:
- backward-compatible changes
- additive evolution
- version stability

Avoid:
- breaking contracts unexpectedly
- changing response structures without versioning

---

# AI Code Generation Rules

AI-generated APIs must:
- follow REST semantics
- generate structured responses
- use proper HTTP status codes
- include validation
- support traceability

Do not generate:
- inconsistent responses
- generic endpoints
- framework-leaking APIs
- unvalidated inputs

---

# Long-Term API Governance

APIs become:
- integration contracts
- frontend dependencies
- platform boundaries

API consistency is critical for:
- microservices
- frontend applications
- third-party integrations
- long-term maintainability
