# Implementation Plan: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

[Extract from feature spec: primary requirement + technical approach from research]

## Technical Context

<!--
  ACTION REQUIRED: Replace the content in this section with the technical details
  for the project. The structure here is presented in advisory capacity to guide
  the iteration process.
-->

**Language/Version**: [e.g., Python 3.11, Swift 5.9, Rust 1.75 or NEEDS CLARIFICATION]
**Primary Dependencies**: [e.g., FastAPI, UIKit, LLVM or NEEDS CLARIFICATION]
**Storage**: [if applicable, e.g., PostgreSQL, CoreData, files or N/A]
**Testing**: [e.g., pytest, XCTest, cargo test or NEEDS CLARIFICATION]
**Architecture**: [Clean architecture layers/boundaries selected, or NEEDS CLARIFICATION]
**Design Patterns**: [Use-case pattern choices with rationale, or NEEDS CLARIFICATION]
**Target Platform**: [e.g., Linux server, iOS 15+, WASM or NEEDS CLARIFICATION]
**Project Type**: [e.g., library/cli/web-service/mobile-app/compiler/desktop-app or NEEDS CLARIFICATION]
**Performance Goals**: [domain-specific, e.g., 1000 req/s, 10k lines/sec, 60 fps or NEEDS CLARIFICATION]
**Constraints**: [domain-specific, e.g., <200ms p95, <100MB memory, offline-capable or NEEDS CLARIFICATION]
**Scale/Scope**: [domain-specific, e.g., 10k users, 1M LOC, 50 screens or NEEDS CLARIFICATION]

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- **Specification source of truth**: Confirm `spec.md` contains prioritized user
  stories, functional requirements, assumptions, edge cases, and measurable success
  criteria, with unresolved ambiguity marked `NEEDS CLARIFICATION`.
- **Independent story slices**: Confirm the P1 story is a usable MVP and each story
  can be implemented, tested, demonstrated, and delivered independently whenever
  practical.
- **Verification planned first**: Define automated tests for stable repeatable
  behavior. Every function introduced by implementation must map to automated
  coverage through unit, component, contract, or integration tests.
- **Technical decisions recorded**: Document architecture, dependencies, structure,
  constraints, design patterns, and complexity tradeoffs before task generation.
- **Clean architecture boundaries**: Confirm domain/business rules do not depend on
  UI, database, network, framework, or AI-provider code; use cases define ports;
  adapters isolate external systems; framework code remains at the outer edge.
- **Pattern fitness per use case**: For each use case, name the chosen pattern
  (plain function/service, command, strategy, repository, adapter, factory, etc.)
  and justify why it is simpler or safer than the alternatives.
- **Traceability and operations**: Ensure planned tasks can trace to stories,
  requirements, contracts, entities, or cross-cutting concerns, and include logging,
  error handling, configuration, security, and performance work when relevant.

## Project Structure

### Documentation (this feature)

```text
specs/[###-feature]/
|-- plan.md              # This file (/speckit-plan command output)
|-- research.md          # Phase 0 output (/speckit-plan command)
|-- data-model.md        # Phase 1 output (/speckit-plan command)
|-- quickstart.md        # Phase 1 output (/speckit-plan command)
|-- contracts/           # Phase 1 output (/speckit-plan command)
`-- tasks.md             # Phase 2 output (/speckit-tasks command; not created by /speckit-plan)
```

### Source Code (repository root)

<!--
  ACTION REQUIRED: Replace the placeholder tree below with the concrete layout
  for this feature. The delivered plan must use clean architecture boundaries,
  remove unused options, and reference real project paths.
-->

```text
# [REMOVE IF UNUSED] Option 1: Single clean architecture project (DEFAULT)
src/
|-- domain/              # Entities, value objects, domain services
|-- application/         # Use cases, ports, DTOs, orchestration
|-- infrastructure/      # Database, network, AI providers, external services
|-- interfaces/          # CLI, HTTP, UI controllers, presenters
`-- shared/              # Cross-cutting utilities with no inward dependencies

tests/
|-- unit/
|   |-- domain/
|   `-- application/
|-- contract/
|-- integration/
`-- architecture/        # Dependency-rule and boundary tests

# [REMOVE IF UNUSED] Option 2: Web application
backend/
|-- src/
|   |-- domain/
|   |-- application/
|   |-- infrastructure/
|   `-- interfaces/
`-- tests/

frontend/
|-- src/
|   |-- domain/
|   |-- application/
|   |-- infrastructure/
|   |-- interfaces/
|   `-- ui/
`-- tests/

# [REMOVE IF UNUSED] Option 3: Mobile + API
api/
`-- [same clean architecture layout as backend above]

ios/ or android/
`-- [platform-specific clean architecture modules, UI flows, and platform tests]
```

**Structure Decision**: [Document the selected clean architecture structure and
reference the real directories captured above]

## Use-Case Design

| Use Case | Pattern / Structure | Boundary Ports | Why This Pattern Fits | Simpler Alternative Rejected |
|----------|---------------------|----------------|-----------------------|------------------------------|
| [UC-001] | [e.g., Interactor + Repository Port] | [Input/output ports] | [Rationale] | [Alternative and reason] |

## Test Strategy

| Scope | Required Coverage | Test Location |
|-------|-------------------|---------------|
| Functions | Every implemented function has automated coverage for normal, boundary/error, or delegation behavior | tests/unit/ or higher-level test when direct unit test adds no value |
| Use cases | Each use case has behavior tests for success and failure paths | tests/unit/application/ or tests/integration/ |
| Boundaries | Ports, adapters, contracts, and dependency rules are verified | tests/contract/, tests/integration/, tests/architecture/ |

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., domain depends on framework type] | [current need] | [why a port/adapter is insufficient] |
| [e.g., Repository pattern] | [specific problem] | [why direct persistence access is sufficient or insufficient] |
