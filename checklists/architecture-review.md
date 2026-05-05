# Architecture Review Checklist

Use this checklist before implementation starts and before merging code.

## Spec Kit Alignment

- [ ] The change traces to a user story, requirement, task, or documented
      cross-cutting concern.
- [ ] The current plan names the architecture and use-case pattern.
- [ ] Any architecture exception is documented in Complexity Tracking.

## Clean Architecture

- [ ] Domain code has no framework, UI, database, network, or AI-provider imports.
- [ ] Application use cases depend on domain and ports, not concrete adapters.
- [ ] Infrastructure implements ports and does not own business rules.
- [ ] Interfaces/UI translate input and output without bypassing use cases.
- [ ] Provider-specific types do not leak into domain or application APIs.
- [ ] Architecture/import-boundary tests exist or were updated.

## Design Patterns

- [ ] Each non-trivial pattern is named.
- [ ] The selected pattern fits the use case.
- [ ] A simpler alternative was considered.
- [ ] No pattern was added only for future speculation.

## Reuse

- [ ] Existing classes, components, hooks, presenters, or adapters were searched.
- [ ] Existing contracts were reused where they fit.
- [ ] New abstractions have a clear owner and stable responsibility.
- [ ] New screens compose existing components where practical.
