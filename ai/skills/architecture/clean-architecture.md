# Clean Architecture Standards

## Objective

Define the architectural structure and dependency rules for all backend services.

The architecture must prioritize:
- maintainability
- modularity
- testability
- scalability
- domain isolation

---

# Architectural Style

Services must follow:
- Clean Architecture principles
- Domain-oriented modular design
- Explicit dependency direction

Preferred structure:
- modular monolith initially
- microservice-ready boundaries
- domain-first organization

---

# Dependency Rule

Dependencies must always point inward.

Outer layers may depend on inner layers.

Inner layers must NEVER depend on:
- frameworks
- infrastructure
- controllers
- databases
- external services

Business logic must remain framework-independent.

---

# Layer Definitions

## Domain Layer

Contains:
- business rules
- domain entities
- value objects
- business invariants
- domain services

The domain layer must:
- contain no framework annotations when possible
- avoid infrastructure dependencies
- remain pure business logic

Avoid:
- database logic
- HTTP concerns
- serialization concerns

---

## Application Layer

Responsible for:
- use cases
- orchestration
- transaction coordination
- validation orchestration

Contains:
- application services
- commands
- queries
- DTO coordination

The application layer:
- coordinates workflows
- invokes domain logic
- handles transactional boundaries

Avoid:
- persistence implementation details
- controller logic

---

## Infrastructure Layer

Responsible for:
- persistence
- messaging
- security
- external integrations
- framework configuration

Contains:
- JPA repositories
- Kafka producers
- REST clients
- security adapters
- database configuration

Infrastructure is replaceable.

---

## Interface Layer

Responsible for:
- REST APIs
- request mapping
- response formatting
- validation entry points

Contains:
- controllers
- request DTOs
- response DTOs
- API documentation

Controllers must remain thin.

Controllers should:
- validate requests
- delegate to application services
- return standardized responses

Avoid:
- business logic
- persistence logic
- transaction logic

---

# Package Organization

Use domain-oriented packaging.

Preferred:

com.company.platform
├── account
│   ├── domain
│   ├── application
│   ├── infrastructure
│   └── interfaces
│
├── payment
├── notification
└── common

Avoid global technical packaging:

- controller/
- service/
- repository/

This structure does not scale well.

---

# Domain Design Principles

Domains must:
- encapsulate business rules
- own their invariants
- expose clear boundaries

Prefer:
- rich domain models
- explicit business methods
- meaningful naming

Avoid:
- anemic entities
- procedural domain logic
- generic utility-driven design

---

# Transaction Boundaries

Transactions must:
- exist in the application layer
- remain explicit
- protect business consistency

Avoid:
- transaction management inside controllers
- transaction leakage across domains

---

# DTO Rules

Always separate:
- domain entities
- request DTOs
- response DTOs

Never expose:
- JPA entities directly
- internal persistence structures

---

# Mapping Rules

Preferred:
- MapStruct

Mapping responsibilities:
- DTO ↔ domain
- domain ↔ persistence
- external ↔ internal models

Avoid:
- excessive manual mapping duplication
- leaking infrastructure models into domain logic

---

# Validation Rules

Validation occurs at multiple levels.

## Interface Validation
Use:
- Jakarta Validation

Example:
- @NotNull
- @NotBlank
- @Email

## Domain Validation
Business invariants belong inside the domain.

Example:
- balance cannot become negative
- journal entries must balance

---

# Exception Handling

Business exceptions belong in:
- domain
or
- application layers

Infrastructure exceptions must not leak directly to APIs.

Use centralized exception handling.

---

# Infrastructure Isolation

Infrastructure concerns must remain isolated.

Examples:
- database technology
- Kafka
- Redis
- Keycloak
- external APIs

The domain should not know implementation details.

---

# Framework Isolation

Business logic should remain minimally coupled to:
- Spring Boot
- JPA
- messaging frameworks

This improves:
- testability
- maintainability
- portability

---

# Modularity Principles

Modules should:
- communicate through explicit contracts
- minimize coupling
- maximize cohesion

Prefer:
- small focused modules
- explicit interfaces
- bounded contexts

Avoid:
- circular dependencies
- shared mutable modules
- hidden cross-domain access

---

# AI Code Generation Rules

When generating architecture:
- prioritize readability
- generate explicit boundaries
- maintain dependency direction
- avoid unnecessary abstraction

Do not:
- generate massive generic base classes
- overuse inheritance
- create speculative abstractions
- collapse all logic into services

---

# Long-Term Evolution

Services should evolve toward:
- event-driven integration
- microservice extraction
- distributed workflows

without requiring major rewrites.

The modular monolith structure should naturally support future decomposition.
