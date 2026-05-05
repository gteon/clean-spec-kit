# AI Code Review Checklist

Use this checklist when code was generated or heavily modified by AI.

## Traceability

- [ ] The generated code maps to a Spec Kit task.
- [ ] The task maps to a requirement or user story.
- [ ] The implementation does not add unrequested behavior.

## Architecture

- [ ] Clean architecture dependency direction still holds.
- [ ] AI/provider code is isolated behind ports and adapters.
- [ ] Domain and application layers remain provider-agnostic.
- [ ] New classes or components have a clear reason to exist.

## Safety

- [ ] No secrets, local paths, or credentials were introduced.
- [ ] AI output is validated before use.
- [ ] Error handling is explicit.
- [ ] Logs do not expose sensitive data.

## Tests

- [ ] Every changed function has automated coverage.
- [ ] Tests cover malformed or unexpected AI output when relevant.
- [ ] Tests use fakes or fixtures instead of live model calls.
- [ ] Relevant tests were run and results are documented.
