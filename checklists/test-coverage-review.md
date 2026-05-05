# Test Coverage Review Checklist

Use this checklist for every code change.

## Function Coverage

- [ ] Every implemented function has automated coverage.
- [ ] Normal behavior is tested.
- [ ] Boundary or error behavior is tested.
- [ ] Delegation-only functions are covered by contract, component, or integration
      tests when direct unit tests add no meaningful assertion.

## Use-Case Coverage

- [ ] Success path is tested.
- [ ] Validation failure is tested.
- [ ] Dependency failure is tested.
- [ ] Permission or approval behavior is tested when relevant.

## Boundary Coverage

- [ ] Ports have contract tests where useful.
- [ ] Adapters test mapping to and from external systems.
- [ ] AI-provider adapters use deterministic fakes or fixtures.
- [ ] Architecture dependency rules are tested.

## Test Quality

- [ ] Tests fail for the intended reason before implementation.
- [ ] Tests assert behavior, not implementation noise.
- [ ] Tests are deterministic.
- [ ] No assertions were weakened to make generated code pass.
- [ ] Skipped tests have a documented reason.
