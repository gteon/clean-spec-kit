# Release Readiness Checklist

Use before merging or deploying a feature.

## Product Readiness

- [ ] P1 user story works independently.
- [ ] Acceptance scenarios pass.
- [ ] Success criteria can be measured.
- [ ] Known limitations are documented.

## Engineering Readiness

- [ ] Formatting passed.
- [ ] Linting/static analysis passed where configured.
- [ ] Unit tests passed.
- [ ] Contract tests passed when boundaries changed.
- [ ] Integration tests passed when workflows changed.
- [ ] Architecture tests passed when source dependencies changed.
- [ ] Coverage did not regress.

## Architecture Readiness

- [ ] Domain remains independent.
- [ ] Use cases go through ports.
- [ ] Adapters isolate external systems.
- [ ] UI/screens compose existing components where practical.
- [ ] Design-pattern choices match the plan.

## Security and AI Readiness

- [ ] No secrets are committed.
- [ ] AI output validation is tested.
- [ ] Provider failures are handled.
- [ ] Sensitive data is not logged.
- [ ] Human approval points are respected.
