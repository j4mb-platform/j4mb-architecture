# Repository Standards

## Objective

Define repository structure, documentation standards, branching strategy, and engineering conventions across all J4MB repositories.

These standards ensure:
- consistency
- discoverability
- maintainability
- onboarding simplicity
- AI generation alignment

---

# Repository Principles

Repositories must be:
- focused
- modular
- self-documenting
- reproducible
- automation-friendly

Each repository should represent:
- a bounded context
- a platform capability
- a clearly scoped engineering concern

Avoid:
- monolithic unrelated repositories
- mixed responsibilities
- undocumented structures

---

# Repository Naming Standards

Use:
- lowercase
- hyphen-separated
- domain-oriented naming

Examples:
- j4mb-ledger
- j4mb-payment
- j4mb-document-service
- j4mb-architecture

Avoid:
- camelCase
- vague repository names
- generic naming

Avoid:
- backend-final
- test-service
- microservice-demo

---

# Standard Repository Structure

Preferred structure:

/
├── src/
├── docs/
├── docker/
├── scripts/
├── .github/
├── README.md
├── LICENSE
├── .gitignore
├── docker-compose.yml
└── pom.xml

---

# Documentation Standards

Every repository must contain:
- clear README
- architecture documentation
- setup instructions
- development workflow

Repositories should remain:
- self-explanatory
- independently understandable

---

# README Standards

Every README must contain:

1. Project Overview
2. Architecture Summary
3. Technology Stack
4. Local Development Setup
5. Running Instructions
6. Environment Variables
7. API Documentation
8. Testing Instructions
9. Folder Structure
10. Roadmap

---

# docs/ Standards

Use:

docs/
├── architecture.md
├── domain-model.md
├── database-design.md
├── api-design.md
├── decisions/
└── diagrams/

---

# Architecture Decision Records (ADR)

Use ADRs for:
- architectural choices
- technology decisions
- infrastructure direction
- tradeoff documentation

Naming:

adr-001-postgresql.md
adr-002-kafka.md

ADRs must include:
- context
- decision
- consequences

---

# diagrams/ Standards

Store:
- architecture diagrams
- sequence diagrams
- domain diagrams
- deployment diagrams

Preferred formats:
- Mermaid
- PlantUML
- draw.io exports

---

# Source Code Organization

Use:
- domain-oriented modular structure

Avoid:
- global technical packaging

Preferred:

com.j4mb.ledger.account
com.j4mb.ledger.transaction

Avoid:
com.j4mb.service.impl.common

---

# Git Branching Strategy

Preferred branches:

- main
- develop
- feature/*
- hotfix/*
- release/*

Examples:
- feature/account-api
- feature/multi-tenant-support
- hotfix/journal-balance-fix

---

# Commit Standards

Use conventional commits.

Examples:

feat: add account creation endpoint
fix: correct transaction validation
refactor: simplify tenant resolution
docs: add architecture overview
test: add account service integration tests

Avoid:
- random commit messages
- vague commit names

Avoid:
- update
- changes
- fix stuff

---

# Pull Request Standards

PRs must include:
- clear summary
- scope description
- testing notes
- architecture impact if applicable

PRs should remain:
- small
- focused
- reviewable

Avoid:
- massive unrelated PRs

---

# .gitignore Standards

Repositories must exclude:

- target/
- .idea/
- .vscode/
- *.iml
- logs/
- .env
- secrets/
- node_modules/

Never commit:
- credentials
- certificates
- secrets
- private keys
- environment-specific configs

---

# Environment Configuration

Use:
- application.yml
- profile-based configuration
- environment variables

Never hardcode:
- secrets
- database passwords
- API keys

---

# Docker Standards

Repositories should contain:
- Dockerfile
- docker-compose.yml

Containers must:
- support local development
- remain reproducible
- include health checks when possible

---

# CI/CD Standards

Repositories should support:
- automated builds
- automated tests
- linting
- static analysis

Preferred:
- GitHub Actions

---

# Testing Standards

Repositories must support:
- unit testing
- integration testing

Preferred tools:
- JUnit 5
- Mockito
- Testcontainers

---

# Dependency Management

Use:
- latest stable LTS dependencies
- explicit dependency management

Avoid:
- outdated libraries
- duplicate dependencies
- unnecessary frameworks

---

# Security Standards

Repositories must:
- avoid sensitive data exposure
- support secure configuration
- isolate secrets from source control

Use:
- environment variables
- secret management tools

Never commit:
- .env production files
- tokens
- credentials

---

# AI Integration Standards

Repositories should contain:
- AI skills
- architectural guidance
- generation rules
- coding standards

Recommended structure:

/ai
├── skills/
├── templates/
└── prompts/

---

# Observability Standards

Services should support:
- structured logging
- metrics
- tracing
- health monitoring

---

# Long-Term Maintainability

Repositories must optimize for:
- incremental evolution
- architectural clarity
- onboarding simplicity
- operational stability

Repositories should remain understandable years later.
