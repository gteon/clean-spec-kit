# Testing Strategy

Tests are the safety net for AI-generated code. They are not optional project
decoration. They are the mechanism that prevents convincing but incorrect code
from reaching users.

## Required Test Layers

### Unit Tests

Use for:

- Domain entities and value objects
- Pure functions
- Use cases with fake ports
- Validation and error handling
- Reusable components with deterministic behavior

### Contract Tests

Use for:

- Application ports
- API contracts
- Adapter expectations
- AI-provider response parsing
- Serialization and deserialization boundaries

### Integration Tests

Use for:

- Real adapter wiring
- Persistence flows
- HTTP/API workflows
- CLI workflows
- Component integration across layers

### Architecture Tests

Use for:

- Forbidden imports
- Layer dependency direction
- Provider SDK isolation
- UI and infrastructure not leaking into domain/application

### End-to-End Tests

Use only when the user workflow cannot be proven with lower-level tests.

## Function-Level Coverage Rule

Every implemented function must be covered by automated tests for at least one of:

- Normal behavior
- Boundary behavior
- Error behavior
- Delegation contract

Direct unit tests are preferred. Higher-level tests are acceptable for framework
hooks, generated glue, or thin pass-through functions only when unit tests would
add no meaningful assertion.

## AI-Specific Testing

AI-facing code must be tested deterministically.

- Use fake model clients for use-case tests.
- Use fixtures for model responses.
- Test malformed, empty, and unsafe model output.
- Test parser failures and retry behavior.
- Test provider errors, timeouts, and rate limits.
- Keep prompts and parsing out of domain tests.

## Coverage Policy

Do not chase a single universal percentage before a stack exists. Instead:

- Require coverage for every changed function.
- Add a numeric threshold once a language and test runner are chosen.
- Never reduce coverage without documenting why.
- Never remove assertions to improve coverage metrics.
