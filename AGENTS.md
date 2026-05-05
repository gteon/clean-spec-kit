# AGENTS.md

Guidance for Codex and other coding agents working in this repository.

<!-- SPECKIT START -->
For additional context about technologies to be used, project structure,
shell commands, and other important information, read the current plan.
<!-- SPECKIT END -->

## Required Reading Order

Before generating or changing code, read the relevant Spec Kit artifacts in this
order:

1. `.specify/memory/constitution.md`
2. The current feature `spec.md`
3. The current feature `plan.md`
4. The current feature `tasks.md`

If a required artifact is missing, do not invent architecture or scope. Create or
update the missing Spec Kit artifact first.

## Source of Truth

Spec Kit artifacts drive implementation:

- `spec.md` defines user value, requirements, assumptions, and success criteria.
- `plan.md` defines architecture, technology choices, design patterns, structure,
  constraints, and test strategy.
- `tasks.md` defines the dependency-ordered implementation work.

Do not implement behavior that is not traceable to a requirement, user story,
contract, or explicitly documented cross-cutting concern.

## Clean Architecture Rules

All production code must follow clean architecture dependency rules unless the
current plan documents and justifies an exception.

Expected default layers:

- `domain`: entities, value objects, pure business rules, domain services.
- `application`: use cases, interactors, ports, DTOs, orchestration.
- `infrastructure`: database, network, file system, AI providers, external APIs.
- `interfaces`: HTTP, CLI, controllers, presenters, view models, UI entry points.
- `ui`: reusable visual components and screens when a frontend exists.
- `shared`: framework-independent utilities that do not create inward dependency
  violations.

Dependency direction must point inward:

- `domain` must not depend on application, infrastructure, interfaces, UI,
  frameworks, databases, network clients, or AI providers.
- `application` may depend on `domain` and its own ports, but not on concrete
  infrastructure or UI.
- `infrastructure` implements application ports and adapts external systems.
- `interfaces` and `ui` call use cases and translate input/output.
- Provider-specific types must not leak into domain or use-case APIs.

Add or update architecture boundary tests whenever a change could weaken these
rules.

## Design Pattern Rules

Use the pattern that best fits the use case, domain behavior, expected growth,
extension points, testing strategy, and clean architecture boundaries. AI agents
should not avoid complete patterns because they require more files; the priority is
future-safe extensibility and maintainable change.

Common choices:

- Domain function: pure calculation or validation with no orchestration.
- Use case/interactor: application workflow, authorization boundary, transaction,
  or side-effect orchestration.
- Port and adapter: database, AI provider, network service, file system, clock,
  random generator, queue, or any external dependency.
- Repository: persistence abstraction for aggregate or entity retrieval/storage.
- Specification: business rules that must be combined, reused, or expanded.
- Pipeline: ordered processing stages, validation stages, enrichment, or AI output
  processing.
- Chain of Responsibility: rule handlers or fallback handlers that can grow over
  time.
- Composite: hierarchical rules, menus, screens, permissions, or nested structures.
- Strategy: interchangeable algorithm, policy, ranking, prompt strategy, or
  provider behavior.
- Command: actions that need validation, authorization, queuing, undo, retry, or
  auditability.
- Builder: construction with many optional parts, steps, or valid combinations.
- Factory: construction is complex, conditional, or must hide infrastructure
  details.
- Abstract Factory: related families of adapters, components, or provider-specific
  implementations.
- Decorator: layered behavior such as logging, caching, retries, metrics, or
  authorization around an existing port/use case.
- Facade: stable API over multiple subsystems or external provider details.
- Observer/Event Publisher: domain or application events consumed by independent
  subscribers.
- State: workflows where valid behavior changes by lifecycle state.
- Presenter/view model: UI-specific formatting that must stay out of domain and
  use cases.

Every non-trivial pattern must be named in the plan or task context and justified
by fit: behavior modeled, extension path, test strategy, and tradeoffs.

Use `docs/design-patterns.md` as the pattern catalog when planning or reviewing
implementation choices.

## Testing Rules

Tests are the deployment safety net for AI-generated code.

- Write tests before implementation whenever creating or changing behavior.
- Every implemented function must have automated coverage for its normal path,
  boundary or error path, or delegation contract.
- Trivial framework hooks, generated glue, and declarations with no executable
  branch may be covered by a higher-level component or integration test only when
  direct unit tests add no meaningful assertion.
- Use-case tests must cover success, expected failure, validation, and dependency
  failure paths.
- Adapter tests must verify mapping between external systems and application
  ports.
- Architecture tests must verify forbidden dependencies.
- Do not mark a task complete while relevant tests fail, are skipped without a
  documented reason, or have not been run.

Prefer fast unit tests for domain and application logic. Add contract,
integration, and end-to-end tests where boundaries or user workflows require them.

## Reuse and Extensibility

Before creating a new class, function, screen, or component:

1. Search for an existing equivalent.
2. Reuse or extend existing abstractions when their contract fits.
3. Prefer composition over inheritance for UI and application behavior.
4. Keep public contracts stable; add new inputs or adapters rather than breaking
   existing callers when practical.
5. Place reusable UI behavior in components, hooks, presenters, or view models so
   new screens can compose existing pieces.

New screens should primarily assemble existing components and call existing use
cases. New components should be small, typed, accessible, and free of direct
infrastructure access.

## AI Integration Rules

AI output is untrusted until validated.

- Isolate model/provider calls behind application ports and infrastructure
  adapters.
- Keep prompts, parsing, retries, and provider-specific options out of domain.
- Validate and sanitize AI output before it reaches domain state or persistence.
- Test AI-facing code with deterministic fakes, fixtures, or contract tests.
- Never hardcode secrets, credentials, or user-specific paths.

## Code Quality Gates

Before finishing a code task:

1. Run formatting and linting if configured.
2. Run relevant unit, contract, integration, and architecture tests.
3. Confirm changed code is traceable to the Spec Kit task.
4. Confirm no unrelated files were modified.
5. Document any test that could not be run and why.

Do not weaken tests, remove assertions, or bypass quality gates to make generated
code pass.
