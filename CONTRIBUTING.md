# Contributing

This repository is designed for human developers and AI coding agents working
together. The quality bar is intentionally strict because generated code can look
correct while hiding architectural coupling or missing test coverage.

## Contribution Flow

1. Start from a Spec Kit feature specification.
2. Clarify ambiguous requirements before planning.
3. Record architecture, design patterns, dependencies, and test strategy in the
   feature plan.
4. Generate or write tasks from the plan.
5. Write failing tests before implementation.
6. Implement one task or logical group at a time.
7. Run the relevant quality gates.
8. Open a pull request using the provided PR template.

## Required Standards

- Do not implement behavior that is not traceable to `spec.md`, `plan.md`, or
  `tasks.md`.
- Follow clean architecture boundaries unless the plan documents a justified
  exception.
- Use the design pattern that best fits the use case, expected growth, extension
  points, and testing needs.
- Do not introduce a repository, factory, strategy, event bus, or service layer
  only because it is familiar.
- Every implemented function must have automated coverage for normal behavior,
  boundary or error behavior, or delegation behavior.
- New screens should compose existing components and call use cases through
  established boundaries.
- New components should be reusable, typed where the language supports it,
  accessible, and free of infrastructure access.
- AI-provider calls must stay behind application ports and infrastructure
  adapters.
- Never commit `.env`, `.env.*`, API keys, private keys, tokens, credentials, or
  user-specific local paths. Use `.env.example` with placeholders instead.

## Architecture Expectations

The default dependency direction is inward:

```text
interfaces/ui -> application -> domain
infrastructure -> application -> domain
```

The domain layer must not import frameworks, databases, network clients, UI code,
or AI-provider SDKs.

## Testing Expectations

Use the fastest meaningful test at the lowest stable layer:

- Domain rules: unit tests.
- Use cases: unit tests with fakes for ports.
- Adapters: contract or integration tests.
- User workflows: integration or end-to-end tests when relevant.
- Dependency boundaries: architecture/import-rule tests.

Do not remove assertions, weaken tests, or mark tests skipped only to make AI
generated code pass.

## Pull Request Expectations

Every pull request must explain:

- Which Spec Kit task or requirement it implements.
- Which layers changed.
- Which design pattern was used and why.
- Which tests were added or updated.
- Which quality gates were run.

If a quality gate could not be run, document the reason and the residual risk.
