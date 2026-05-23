# Naming Conventions

## Objective

Define consistent naming conventions across:
- backend services
- APIs
- databases
- events
- infrastructure
- AI-generated code

Naming consistency improves:
- readability
- maintainability
- discoverability
- operational clarity
- large-scale architecture evolution

---

# General Naming Principles

Names must:
- reveal intent
- use domain language
- remain explicit
- stay consistent

Prefer:
- business terminology
- descriptive naming
- predictable patterns

Avoid:
- abbreviations
- ambiguous names
- technical jargon leakage
- inconsistent pluralization

---

# Package Naming

Use:
- lowercase
- domain-oriented structure

Preferred:

com.j4mb.ledger.account
com.j4mb.payment.transaction

Avoid:
- generic technical packaging
- deep unnecessary nesting

Avoid:
com.j4mb.service.impl.utils.common

---

# Module Naming

Modules should use:
- business domain names

Examples:
- account
- payment
- notification
- tenant
- document

Avoid:
- misc
- sharedstuff
- manager
- util

---

# Class Naming

Use:
- PascalCase

Examples:
- AccountService
- PaymentController
- JournalEntryRepository

Class names must represent:
- business responsibility
- architectural role

---

# Interface Naming

Use meaningful capability-based names.

Examples:
- PaymentProcessor
- NotificationSender
- TenantResolver

Avoid:
- IService
- IManager

---

# Method Naming

Methods should describe behavior clearly.

Examples:
- createAccount()
- postTransaction()
- calculateBalance()
- findByTenantId()

Avoid:
- process()
- execute()
- doWork()
- handleData()

---

# Variable Naming

Variables must:
- explain purpose
- use domain language

Examples:
- tenantId
- accountNumber
- journalEntryId
- transactionAmount

Avoid:
- obj
- temp
- data
- value

---

# Constant Naming

Use:
- UPPER_SNAKE_CASE

Examples:
- MAX_RETRY_COUNT
- DEFAULT_PAGE_SIZE
- TOKEN_EXPIRATION_MINUTES

Avoid magic numbers and hardcoded strings.

---

# REST API Naming

## Resource Naming

Use:
- plural resource names
- lowercase
- kebab-case only if necessary

Preferred:

/api/v1/accounts
/api/v1/payments
/api/v1/journal-entries

Avoid:
- verbs in endpoints
- mixed naming styles

Avoid:
- /getAccounts
- /createPayment

---

# REST Path Variables

Use explicit resource identifiers.

Examples:

/accounts/{accountId}
/tenants/{tenantId}/users

Avoid:
- generic ids without context

---

# DTO Naming

## Request DTOs

Examples:
- CreateAccountRequest
- UpdatePaymentRequest

## Response DTOs

Examples:
- AccountResponse
- PaymentDetailsResponse

Avoid:
- generic DTO naming

Avoid:
- AccountDTO
- PaymentData

---

# Entity Naming

Entities must use:
- singular nouns

Examples:
- Account
- Transaction
- JournalEntry

Avoid:
- Accounts
- TransactionEntity

---

# Repository Naming

Use:
<EntityName>Repository

Examples:
- AccountRepository
- PaymentRepository

Avoid:
- GenericRepository
- MainRepository

---

# Service Naming

Use:
<Entity/Capability>Name + Service

Examples:
- AccountService
- PaymentService
- NotificationService

Avoid:
- ServiceImpl naming exposure
- GenericService

---

# Exception Naming

Exceptions must describe business failures.

Examples:
- AccountNotFoundException
- InsufficientBalanceException
- TenantAccessDeniedException

Avoid:
- GenericBusinessException
- ValidationFailedException

---

# Event Naming

Events must represent completed business facts.

Use:
<PastTenseBusinessEvent>

Examples:
- AccountCreated
- PaymentProcessed
- InvoiceGenerated
- TenantProvisioned

Avoid:
- CreateAccountEvent
- PaymentEvent
- ProcessInvoiceEvent

Events describe:
- something that already happened

---

# Kafka Topic Naming

Use:
domain.entity.action.v1

Examples:
- ledger.account.created.v1
- payment.transaction.completed.v1
- notification.email.sent.v1

Requirements:
- lowercase
- dot-separated
- versioned

Avoid:
- random naming
- mixed separators
- unversioned topics

---

# Database Naming

## Table Naming

Use:
- snake_case
- plural table names

Examples:
- accounts
- journal_entries
- payment_transactions

---

## Column Naming

Use:
- snake_case

Examples:
- tenant_id
- created_at
- account_number

Avoid:
- camelCase columns
- inconsistent abbreviations

---

# Primary Key Naming

Preferred:
- id

Foreign keys:
- account_id
- tenant_id
- payment_id

Avoid:
- inconsistent key naming

---

# Audit Field Naming

Standard audit fields:

- created_at
- created_by
- updated_at
- updated_by
- deleted_at

---

# Migration Naming

Flyway migrations:

V1__init.sql
V2__create_accounts_table.sql
V3__add_tenant_support.sql

Requirements:
- sequential
- descriptive
- immutable after execution

---

# Docker Naming

## Container Names

Examples:
- j4mb-postgres
- j4mb-ledger-service

## Network Names

Examples:
- j4mb-network

---

# Kubernetes Naming

Use:
- lowercase
- hyphen-separated

Examples:
- ledger-service
- payment-service

Avoid:
- camelCase
- underscores

---

# Environment Variable Naming

Use:
- UPPER_SNAKE_CASE

Examples:
- DB_HOST
- JWT_SECRET
- KAFKA_BOOTSTRAP_SERVERS

---

# AI Code Generation Rules

AI-generated names must:
- follow domain language
- remain explicit
- avoid abbreviations
- maintain consistency

AI must never generate:
- meaningless names
- temporary naming
- generic utility naming
- unclear abstractions

---

# Long-Term Naming Stability

Names become architectural contracts.

Changing names later impacts:
- APIs
- databases
- integrations
- events
- observability
- documentation

Prefer:
- stable naming
- intentional terminology
- domain consistency

from the beginning.
