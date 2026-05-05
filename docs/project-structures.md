# Project Structures

This starter does not create runtime source folders before a stack is chosen.
These structures are examples for future projects.

## Single Backend, API, CLI, or Library

```text
src/
|-- domain/
|-- application/
|   |-- ports/
|   `-- use_cases/
|-- infrastructure/
|-- interfaces/
`-- shared/

tests/
|-- unit/
|   |-- domain/
|   `-- application/
|-- contract/
|-- integration/
`-- architecture/
```

## Web Application

```text
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
|   |-- ui/
|   `-- shared/
`-- tests/
```

## Screen and Component Reuse

Prefer this flow for new screens:

1. Add or reuse a use case in `application`.
2. Add or reuse a presenter/view model in `interfaces`.
3. Compose existing components in `ui`.
4. Add a new screen only when composition cannot express the workflow.
5. Keep API clients, storage clients, and AI providers out of components.

## Naming Guidance

Names should reflect behavior and boundaries:

- Use cases: `CreateOrder`, `GenerateSpecification`, `ReviewAiOutput`
- Ports: `SpecificationRepository`, `AiModelGateway`, `Clock`
- Adapters: `SqlSpecificationRepository`, `OpenAiModelGateway`
- Components: `SpecificationEditor`, `ReviewPanel`, `ApprovalButton`

Adapt naming conventions to the chosen language.
