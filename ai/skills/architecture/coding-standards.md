# Coding Standards

## Objective

Define coding standards for all backend services to ensure:
- readability
- consistency
- maintainability
- testability
- production-grade quality

These standards apply to:
- handwritten code
- AI-generated code
- generated templates
- refactoring operations

---

# General Principles

Code must prioritize:
- clarity
- simplicity
- explicitness
- consistency

Prefer:
- understandable code
- maintainable structure
- predictable behavior

Avoid:
- clever code
- hidden side effects
- unnecessary abstraction
- premature optimization

---

# Naming Standards

## General Naming Rules

Names must:
- reveal intent
- use business terminology
- remain unambiguous

Prefer:
- meaningful names
- domain-oriented language

Avoid:
- abbreviations
- generic names
- single-letter variables

---

## Class Naming

Use:
- PascalCase

Examples:
- AccountService
- JournalEntry
- PaymentProcessor

Avoid:
- Utils
- Manager
- Helper
- ProcessorFactoryImpl

---

## Method Naming

Methods should describe behavior clearly.

Examples:
- createAccount()
- postJournalEntry()
- calculateBalance()

Avoid:
- process()
- handle()
- executeStuff()

---

## Variable Naming

Variables must explain purpose.

Examples:
- tenantId
- accountBalance
- transactionTimestamp

Avoid:
- data
- value
- obj
- tmp

---

# Method Design

Methods must:
- perform one responsibility
- remain small and focused
- avoid deep nesting

Preferred:
- early returns
- explicit flow
- readable branching

Avoid:
- long procedural methods
- nested condition pyramids
- side-effect-heavy methods

---

# Class Design

Classes should:
- have single responsibility
- remain cohesive
- minimize dependencies

Avoid:
- god classes
- massive services
- static utility dumping grounds

---

# Immutability

Prefer immutability where practical.

Use:
- final fields
- immutable DTOs
- immutable value objects

Avoid:
- unnecessary mutable shared state

---

# Null Handling

Avoid null-heavy design.

Prefer:
- Optional where appropriate
- explicit validation
- defensive programming

Never:
- return null collections
- silently ignore null issues

---

# Error Handling

Errors must be:
- explicit
- meaningful
- traceable

Avoid:
- swallowing exceptions
- empty catch blocks
- generic Exception usage

Use:
- business-specific exceptions
- centralized exception handling

---

# Logging Standards

Logs must:
- provide operational value
- include context
- support debugging

Avoid:
- excessive logging
- duplicated logs
- sensitive information leakage

Never log:
- passwords
- tokens
- secrets
- personal sensitive data

---

# Comments

Code should be self-explanatory.

Use comments only when:
- explaining business rules
- clarifying complex decisions
- documenting non-obvious behavior

Avoid:
- redundant comments
- commented-out code
- noisy inline comments

---

# Formatting Standards

Use:
- consistent indentation
- readable spacing
- logical grouping

Requirements:
- one class per file
- small focused files
- grouped imports

Avoid:
- extremely long files
- excessive horizontal scrolling

---

# DTO Standards

Separate:
- request DTOs
- response DTOs
- domain models
- persistence models

DTOs should:
- remain simple
- avoid business logic

---

# Entity Standards

Entities should:
- encapsulate invariants
- expose meaningful business behavior

Avoid:
- public mutable state
- setter-heavy anemic entities

---

# Service Standards

Services should:
- coordinate business workflows
- remain focused
- delegate properly

Avoid:
- massive orchestration classes
- mixed infrastructure concerns

---

# Controller Standards

Controllers must remain thin.

Controllers should:
- validate input
- delegate work
- return responses

Controllers must NOT:
- contain business logic
- contain persistence logic
- manage transactions

---

# Repository Standards

Repositories should:
- focus on persistence
- expose meaningful query methods

Avoid:
- embedding business logic
- leaking persistence concerns upward

---

# Configuration Standards

Configuration must:
- remain externalized
- support environments
- avoid hardcoded values

Never:
- hardcode credentials
- hardcode secrets

---

# Dependency Injection

Use constructor injection exclusively.

Avoid:
- field injection
- static dependency access

---

# Async Processing

Async operations must:
- remain explicit
- support tracing
- support retry strategies

Avoid:
- hidden async execution
- unmanaged threading

---

# Testability Standards

Code must remain easy to test.

Prefer:
- small focused methods
- explicit dependencies
- deterministic behavior

Avoid:
- hidden global state
- tightly coupled implementations

---

# AI Code Generation Rules

AI-generated code must:
- follow naming conventions
- generate readable methods
- avoid overengineering
- avoid unnecessary abstraction
- remain production-oriented

Do not generate:
- placeholder TODO methods
- fake implementations
- speculative abstractions
- unused generic utilities

---

# Refactoring Principles

Refactoring must:
- preserve behavior
- improve readability
- reduce complexity
- maintain architectural boundaries

Avoid:
- unnecessary rewrites
- broad risky refactors
- abstraction for abstraction’s sake

---

# Long-Term Maintainability

All code should optimize for:
- future understanding
- operational simplicity
- incremental evolution
- team readability

Code is maintained longer than it is written.
