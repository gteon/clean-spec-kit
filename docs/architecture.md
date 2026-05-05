# Architecture Guide

This starter uses clean architecture as the default design model. The goal is not
to add ceremony. The goal is to keep business rules independent, testable, and
easy to evolve as frameworks, screens, databases, and AI providers change.

## Dependency Rule

Dependencies point inward:

```text
interfaces/ui -> application -> domain
infrastructure -> application -> domain
```

Outer layers may depend on inner layers. Inner layers must not depend on outer
layers.

## Layers

### Domain

Owns business concepts and rules.

May contain:

- Entities
- Value objects
- Domain services
- Domain events
- Pure validation and calculation logic

Must not contain:

- Framework imports
- Database queries
- Network clients
- File-system calls
- UI rendering
- AI-provider SDKs
- Environment variables

### Application

Owns use cases and orchestration.

May contain:

- Use cases or interactors
- Input and output DTOs
- Ports/interfaces for external dependencies
- Transaction or workflow coordination
- Authorization decisions when they are application-specific

Must not depend on concrete infrastructure.

### Infrastructure

Owns external systems.

May contain:

- Database adapters
- API clients
- AI-provider clients
- File-system adapters
- Queue adapters
- Email/SMS/payment adapters
- Clock, random, and ID-generation adapters

Infrastructure implements application ports.

### Interfaces and UI

Own entry points and presentation.

May contain:

- HTTP controllers
- CLI commands
- GraphQL resolvers
- View models
- Presenters
- Screens
- Reusable UI components

Interfaces translate external input into use-case input and translate use-case
output into presentation output.

## Pattern Selection

Choose the pattern that best models the domain behavior and expected evolution.
The right pattern is the one that preserves clean architecture boundaries, keeps
the code testable, and lets future rules, screens, providers, and workflows be
added without rewriting stable code.

| Problem | Preferred Pattern |
|---------|-------------------|
| Pure calculation | Domain function |
| User workflow | Use case/interactor |
| External dependency | Port and adapter |
| Data retrieval/storage | Repository when it hides persistence details |
| Expandable business rules | Specification, Composite, or Chain of Responsibility |
| Ordered processing stages | Pipeline |
| Swappable algorithm | Strategy |
| Auditable user action | Command |
| Stepwise construction | Builder |
| Complex object construction | Factory |
| Provider family construction | Abstract Factory |
| Layered cross-cutting behavior | Decorator |
| Stable API over subsystems | Facade |
| Independent reactions to events | Observer/Event Publisher |
| Lifecycle-specific behavior | State |
| UI formatting | Presenter or view model |

If 5 rules today may become 50 rules tomorrow, prefer a pattern that makes adding
the next rule a new class/configuration/stage instead of a risky edit to existing
conditionals.

## Architecture Tests

Every real project should add import/dependency tests that prove:

- Domain imports no outer layer.
- Application imports no concrete infrastructure or UI.
- Infrastructure implements ports instead of being called directly by domain.
- UI and interfaces depend on use cases, not databases or AI providers.

The exact tool depends on the language, but the rule is language-neutral.
