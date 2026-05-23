# Spring Boot Standards

## Objective

Define enterprise-grade Spring Boot standards for all backend services.

These standards ensure:
- consistency
- maintainability
- production readiness
- cloud-native compatibility
- enterprise engineering quality

---

# Spring Boot Version Policy

Always use:
- latest stable Spring Boot 3.x release

Requirements:
- stable releases only
- no milestone versions
- no release candidates

Prefer:
- latest Java LTS support

Current preference:
- Java 21

---

# Java Standards

Use:
- Java 21 LTS

Requirements:
- modern Java features
- records where appropriate
- sealed classes when useful
- strong typing
- immutability preference

Avoid:
- deprecated APIs
- legacy Java patterns
- outdated libraries

---

# Build Tool Standards

Preferred:
- Maven

Requirements:
- deterministic builds
- dependency management
- reproducible environments

Use:
- Maven Wrapper

Required files:
- mvnw
- mvnw.cmd
- .mvn/

---

# Required Core Dependencies

Preferred dependencies:

- spring-boot-starter-web
- spring-boot-starter-validation
- spring-boot-starter-data-jpa
- spring-boot-starter-actuator
- postgresql
- flyway-core
- lombok

Optional based on service:
- spring-boot-starter-security
- spring-kafka
- spring-boot-starter-cache
- springdoc-openapi

Avoid:
- unnecessary starters
- overlapping libraries
- abandoned dependencies

---

# Project Structure

Use domain-oriented modular packaging.

Preferred:

com.j4mb.platform
├── account
├── payment
├── notification
├── common
└── infrastructure

Avoid:
- technical global packaging
- service.impl patterns
- utility dumping structures

---

# Spring Configuration Standards

Use:
- application.yml

Avoid:
- application.properties for complex systems

Configuration must support:
- local
- dev
- test
- staging
- production

Use:
- profile-based configuration

Examples:
- application-local.yml
- application-dev.yml
- application-prod.yml

---

# Environment Variable Standards

Use environment variables for:
- secrets
- credentials
- infrastructure endpoints
- external integrations

Never hardcode:
- passwords
- tokens
- secrets

---

# Bean Management Standards

Use:
- constructor injection only

Avoid:
- field injection
- static bean access

Beans should remain:
- focused
- cohesive
- testable

---

# Controller Standards

Controllers must:
- remain thin
- validate requests
- delegate business logic

Controllers must NOT:
- contain business rules
- contain persistence logic
- manage transactions

Use:
- @RestController
- @RequestMapping
- request validation

---

# Service Standards

Services should:
- orchestrate business workflows
- coordinate domain operations
- remain focused

Avoid:
- massive orchestration services
- infrastructure leakage

---

# Repository Standards

Use:
- Spring Data JPA

Repositories should:
- remain persistence-focused
- expose meaningful queries

Avoid:
- business logic inside repositories

---

# DTO Standards

Always separate:
- request DTOs
- response DTOs
- entities
- domain models

Never expose:
- JPA entities directly in APIs

Preferred:
- immutable DTOs
- Java records where appropriate

---

# Validation Standards

Use:
- Jakarta Validation

Examples:
- @NotNull
- @NotBlank
- @Email
- @Size

All external input must be validated.

Validation must occur:
- at API boundaries
- before business execution

---

# Exception Handling Standards

Use centralized exception handling.

Required:
- @RestControllerAdvice

Requirements:
- standardized error responses
- meaningful HTTP status codes
- traceable error handling

Never:
- expose stack traces
- return raw exceptions

---

# Logging Standards

Use:
- SLF4J
- Logback

Requirements:
- structured logging
- correlation IDs
- tenant context support

Never log:
- passwords
- tokens
- secrets

Avoid excessive debug logging.

---

# Database Standards

Preferred:
- PostgreSQL

Use:
- Flyway migrations

Never use in production:
- ddl-auto=create
- ddl-auto=update

Preferred:
- explicit schema evolution

---

# Transaction Management

Use:
- @Transactional in application layer

Transactions should:
- remain explicit
- remain focused
- protect consistency boundaries

Avoid:
- transaction management in controllers
- long-running transactions

---

# API Standards

Use:
- RESTful APIs
- versioned endpoints

Examples:
- /api/v1/accounts
- /api/v1/payments

Responses must remain:
- structured
- consistent
- documented

---

# OpenAPI Standards

Use:
- springdoc-openapi

Requirements:
- Swagger UI
- endpoint descriptions
- request examples
- response examples

---

# Security Standards

Preferred:
- Spring Security
- JWT authentication
- OAuth2 Resource Server
- Keycloak integration

Requirements:
- stateless authentication
- RBAC authorization
- secure endpoint protection

Never:
- disable security globally
- expose internal APIs publicly

---

# Multi-Tenant Standards

Services should support:
- tenant context propagation
- tenant-aware persistence
- tenant-aware logging

Preferred initial strategy:
- tenant_id discriminator column

Avoid:
- tenant data leakage
- shared tenant state

---

# Async Processing Standards

Use async processing only when justified.

Preferred:
- Kafka for distributed async workflows

Avoid:
- unmanaged async execution
- hidden background processing

---

# Caching Standards

Preferred:
- Redis

Caching must:
- remain explicit
- support invalidation strategies
- remain tenant-aware

Avoid:
- uncontrolled caching
- stale critical financial data

---

# Observability Standards

All services must support:
- health checks
- metrics
- tracing
- structured logs

Use:
- Spring Boot Actuator
- Prometheus
- OpenTelemetry

---

# Docker Standards

Services must provide:
- Dockerfile
- docker-compose support

Requirements:
- lightweight containers
- reproducible environments
- startup consistency

---

# Testing Standards

Required:
- unit tests
- integration tests

Preferred tools:
- JUnit 5
- Mockito
- Testcontainers

Tests must:
- remain deterministic
- support isolated execution

---

# Performance Standards

Services must:
- support pagination
- optimize queries
- avoid N+1 problems
- support connection pooling

Avoid:
- loading large datasets unnecessarily
- blocking operations in critical flows

---

# AI Code Generation Rules

AI-generated Spring Boot code must:
- follow clean architecture
- remain production-oriented
- avoid deprecated APIs
- avoid placeholder logic
- remain readable and testable

Do not generate:
- massive base abstractions
- unnecessary inheritance
- speculative generic frameworks

---

# Enterprise Readiness

Generated services should support future:
- Kubernetes deployment
- CI/CD integration
- event-driven evolution
- distributed tracing
- horizontal scaling

without requiring architectural rewrites.
