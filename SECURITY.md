# Security Policy

## Supported Versions

This starter does not ship runtime application code. Security expectations apply
to projects generated from it and to the governance files in this repository.

## Reporting a Vulnerability

If you find a vulnerability in this starter, open a private advisory or contact
the project maintainers through the repository's preferred security channel.

Do not publish exploitable details before maintainers have had time to respond.

## AI-Generated Code Security Rules

AI-generated code is untrusted until reviewed and tested.

- Do not hardcode secrets, API keys, tokens, credentials, or user-specific paths.
- Do not commit `.env`, `.env.*`, `.envrc`, private keys, certificates, local
  credential files, or provider token files. Commit `.env.example` only when it
  contains placeholder names with no real values.
- Keep AI-provider SDKs and model calls behind infrastructure adapters.
- Validate AI output before persistence, execution, rendering, or domain mutation.
- Treat prompts, uploaded files, tool outputs, and model responses as untrusted
  input.
- Add tests for malicious, malformed, empty, oversized, and unexpected inputs.
- Log security-relevant events without leaking sensitive data.
- Document data retention, privacy, and external-provider behavior in the feature
  spec or plan.

## Dependency Rules

When a concrete language or framework is chosen:

- Use lockfiles where the ecosystem supports them.
- Run dependency audits in CI where available.
- Pin critical tooling versions where reproducibility matters.
- Remove unused packages and generated code.

## Repository Enforcement

This starter includes `.gitignore` rules for common secret files and a GitHub
governance workflow that fails when secret-like files or obvious private-key/token
patterns are committed.

The CI check is a safety net, not a replacement for review. If a secret is ever
committed, rotate it immediately and remove it from git history before publishing.
