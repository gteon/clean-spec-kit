# Quality Gates

Quality gates define what must be true before code is considered ready.

## Before Implementation

- The feature has a `spec.md`.
- Ambiguities are resolved or marked `NEEDS CLARIFICATION`.
- The feature has a `plan.md`.
- The plan documents architecture, design patterns, dependencies, and test
  strategy.
- The feature has `tasks.md`.
- Test tasks appear before implementation tasks.

## Before Completing a Task

- The change maps to a task.
- The code follows clean architecture boundaries.
- The design pattern fits the use case, expected growth, extension points, and
  test strategy.
- Existing components/classes/functions were reused where their contracts fit.
- New behavior has automated tests.
- Relevant tests were run.

## Before Pull Request

- Formatting passes.
- Linting/static analysis passes where configured.
- Unit tests pass.
- Contract tests pass when boundaries changed.
- Integration tests pass when workflows or adapters changed.
- Architecture tests pass when source dependencies changed.
- Security-sensitive behavior has tests.
- AI-facing code uses deterministic fakes or fixtures in tests.

## Before Deployment

- All required CI jobs pass.
- No skipped tests remain without documented justification.
- No architecture boundary exceptions exist outside the plan.
- No secrets or local paths are committed.
- The release/readiness checklist is complete.

## Minimum Generic CI

Before a language is chosen, CI should at least verify repository governance:

- Required docs exist.
- Spec Kit constitution exists.
- Agent guidance exists.
- PR template exists.
- No stale optional-test language exists in templates.
- No generic `models/services` default structure is promoted over clean
  architecture.

After a language is chosen, add stack-specific jobs.
