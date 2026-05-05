# Clean Spec Kit Starter

A language-agnostic starter for building new projects with Spec Kit, Codex,
Claude, clean architecture, appropriate design patterns, and test-first
AI-assisted development.

This is not a framework boilerplate. It intentionally starts before any language,
database, UI library, API framework, or AI provider is chosen. The first feature
plan decides those choices based on product needs.

## Why This Exists

AI-generated code can be fast, but it is not automatically safe, maintainable, or
well-architected. This starter gives humans and AI agents a shared operating
system:

- Spec Kit artifacts define scope before code.
- Clean architecture keeps business rules independent.
- Design patterns must fit the use case, not personal preference.
- Every implemented function must be testable and covered.
- New screens and components should reuse existing classes, components, files, and
  use cases.
- AI providers stay isolated behind ports and adapters.
- Secrets, `.env` files, API keys, and private keys must never be committed.
- GitHub templates and CI protect the quality rules.

## Who Should Use This

Use this starter when creating a fresh:

- Web app
- API
- Backend service
- CLI
- Library
- Mobile app
- AI-assisted product

Do not use this as a drop-in runtime app. It contains governance, templates,
checklists, and workflow files that guide the first real implementation.

## Repository Map

```text
.specify/                 Spec Kit memory, templates, scripts, extensions, workflows
.agents/                  Codex/agent skill definitions for Spec Kit commands
.claude/                  Claude skill definitions for Spec Kit commands
.github/                  PR template, issue templates, governance workflow
docs/                     Architecture, testing, quality, workflow, AI policy docs
docs/decisions/           ADR guidance and template
checklists/               Architecture, testing, AI code, release review checklists
AGENTS.md                 Codex and agent behavior rules
CLAUDE.md                 Claude behavior rules
CONTRIBUTING.md           Contribution and PR standards
SECURITY.md               Security and AI-output safety policy
CODE_OF_CONDUCT.md        Community behavior expectations
SUPPORT.md                Support and question guidance
CHANGELOG.md              Starter changelog
LICENSE                   MIT license
```

## Start a New Project From This Starter

### Option 1: GitHub Template

1. Push this starter to GitHub.
2. In GitHub, mark the repository as a template repository.
3. For a new project, click **Use this template**.
4. Clone the new project locally.

### Option 2: Clone Directly

```bash
git clone https://github.com/YOUR_ORG/YOUR_STARTER_REPO.git my-project
cd my-project
```

After cloning, rename the project and update repository-specific metadata as
needed.

## Codex Integration

Open the project folder in Codex. Codex reads [AGENTS.md](AGENTS.md), which tells
it to use Spec Kit artifacts, clean architecture, justified patterns, test-first
implementation, and quality gates.

Recommended first prompt:

```text
Read AGENTS.md and .specify/memory/constitution.md.
Help me create the first feature with Spec Kit.
Do not choose a language or framework until the plan requires it.
```

Expected Codex flow:

```text
/speckit-specify
/speckit-clarify
/speckit-plan
/speckit-tasks
/speckit-analyze
/speckit-implement
```

Codex should then implement only from generated tasks, write tests before code,
respect clean architecture boundaries, and run the relevant quality gates before
finishing.

## Claude Integration

Claude uses [CLAUDE.md](CLAUDE.md) and the `.claude/skills/` Spec Kit skills.

Recommended first prompt:

```text
Read CLAUDE.md and .specify/memory/constitution.md.
Use the Spec Kit workflow to define and plan my first feature before coding.
```

The project keeps `AGENTS.md` and `CLAUDE.md` aligned so Codex and Claude follow
the same engineering rules.

## Spec Kit Workflow

The intended development flow is:

```text
idea -> spec.md -> clarify -> plan.md -> tasks.md -> analyze -> implement
```

1. **Specify**: capture user stories, requirements, edge cases, assumptions, and
   success criteria.
2. **Clarify**: resolve ambiguous scope, data, privacy, AI behavior, and approval
   points.
3. **Plan**: choose architecture, stack, design patterns, ports/adapters, test
   strategy, and project structure.
4. **Tasks**: create dependency-ordered work with tests before implementation.
5. **Analyze**: check consistency across spec, plan, and tasks.
6. **Implement**: code from tasks only, with tests and quality gates.

See [docs/spec-kit-workflow.md](docs/spec-kit-workflow.md).

## Clean Architecture Default

When a stack is chosen, the default structure is:

```text
src/
|-- domain/              # Entities, value objects, pure business rules
|-- application/         # Use cases, ports, DTOs, orchestration
|-- infrastructure/      # Database, network, AI providers, external systems
|-- interfaces/          # HTTP, CLI, controllers, presenters, view models
|-- ui/                  # Screens and reusable components when a frontend exists
`-- shared/              # Framework-independent shared utilities

tests/
|-- unit/
|-- contract/
|-- integration/
`-- architecture/
```

Dependency direction points inward:

```text
interfaces/ui -> application -> domain
infrastructure -> application -> domain
```

Domain must not depend on frameworks, databases, UI, network clients, file systems,
or AI-provider SDKs.

See [docs/architecture.md](docs/architecture.md) and
[docs/project-structures.md](docs/project-structures.md).

## Design Pattern Standard

Use the simplest pattern that fits the use case:

| Need | Typical Pattern |
|------|-----------------|
| Pure calculation or validation | Plain function |
| User workflow | Use case / interactor |
| External dependency | Port and adapter |
| Persistence abstraction | Repository |
| Swappable algorithm or provider policy | Strategy |
| Complex construction | Factory |
| UI formatting | Presenter or view model |

Every non-trivial pattern must be named in the plan and justified against a
simpler alternative.

## Testing Standard

Tests are mandatory because they prevent humans from deploying bad code generated
by AI.

Required expectations:

- Tests are written before implementation when behavior changes.
- Every implemented function has automated coverage for normal behavior, boundary
  or error behavior, or delegation behavior.
- Use cases cover success, validation failure, expected failure, and dependency
  failure paths.
- Adapters verify mapping to and from external systems.
- Architecture tests verify forbidden dependencies.
- AI-facing tests use deterministic fakes, fixtures, and contract tests instead of
  live model calls.

See [docs/testing-strategy.md](docs/testing-strategy.md).

## Reuse and Extensibility

Before adding a class, function, screen, component, or file:

1. Search for an existing equivalent.
2. Reuse or extend existing contracts when they fit.
3. Prefer composition over inheritance.
4. Keep public contracts stable where practical.
5. Put reusable UI behavior in components, hooks, presenters, or view models.

New screens should mostly compose existing components and call existing use cases.
New components should be small, accessible, typed where the language supports it,
and free of direct infrastructure access.

## GitHub Workflow

This starter includes:

- Pull request template
- Feature, bug, and architecture-change issue templates
- Governance workflow at `.github/workflows/governance.yml`

The governance workflow checks that the starter's required files exist and that
the core templates do not drift back toward weak rules, such as optional tests or
generic `models/services` layering. It also fails when common secret files,
private keys, or obvious provider tokens are committed.

After choosing a stack, add stack-specific CI jobs for formatting, linting, type
checking, tests, coverage, dependency audits, and architecture boundary checks.

See [docs/quality-gates.md](docs/quality-gates.md).

## What This Starter Does Not Include

By design, this starter does not include:

- Runtime source code
- A selected programming language
- A web framework
- A UI component library
- A database
- An AI provider SDK
- Stack-specific CI

Those belong in the first feature plan after requirements are known.

## Files Kept Intentionally

The following folders may look tool-specific, but they are intentional:

- `.specify/`: required for Spec Kit templates, scripts, memory, and workflows.
- `.agents/`: Spec Kit skills for Codex and compatible agent workflows.
- `.claude/`: Spec Kit skills for Claude workflows.
- `.github/`: collaboration templates and governance CI.
- `docs/` and `checklists/`: reusable guidance for humans and AI agents.

No unnecessary starter files are currently known. Avoid deleting these unless you
are intentionally dropping support for that workflow.

## Recommended First PR In a New Project

After creating a project from this starter:

1. Update the project name in README and package metadata once a stack exists.
2. Run the Spec Kit workflow for the first feature.
3. Add stack-specific source folders from the generated plan.
4. Add stack-specific CI jobs.
5. Keep the starter governance files unless the project intentionally changes its
   quality model.

## License

MIT. See [LICENSE](LICENSE).
