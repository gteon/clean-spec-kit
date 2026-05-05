# AI-Generated Code Policy

AI tools may generate, refactor, test, and review code in this project. Their
output is useful, but it is not trusted by default.

## Required Controls

- AI-generated code must be traceable to Spec Kit artifacts.
- AI-generated code must follow the project architecture.
- AI-generated code must be covered by automated tests.
- AI-generated code must be reviewed before deployment.
- AI-generated code must not bypass linting, typing, security, or architecture
  gates.

## Human Approval Points

Human review is required for:

- Architecture changes
- New dependencies
- Security-sensitive logic
- Data retention or privacy behavior
- Authentication or authorization behavior
- Payment, billing, or irreversible workflows
- AI automation that acts on behalf of users

## AI Provider Boundaries

Provider-specific code belongs in infrastructure adapters.

Do not allow provider SDK types, prompt formats, retry settings, or response
schemas to leak into domain or use-case APIs.

## Prompt and Output Safety

- Treat prompts as input.
- Treat model responses as untrusted output.
- Validate and sanitize model output before use.
- Store only what the spec and plan permit.
- Redact sensitive data from logs.

## Test Requirements

Use deterministic tests for AI behavior:

- Fake providers
- Recorded fixtures
- Parser tests
- Error-path tests
- Safety-filter tests
- Contract tests around provider adapters

Do not require live model calls for the normal unit test suite.
