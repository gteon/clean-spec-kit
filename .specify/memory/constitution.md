<!--
Sync Impact Report
Version change: 1.0.0 -> 1.1.0
Modified principles:
- III. Verification Is Planned Before Implementation (expanded to require function-level automated tests)
- IV. Plans Capture Technical Decisions (expanded for fit-for-purpose pattern and extension rationale)
Added sections:
- VI. Clean Architecture Boundaries Are Mandatory
Removed sections:
- None
Templates requiring updates:
- Updated .specify/templates/plan-template.md
- Updated .specify/templates/spec-template.md
- Updated .specify/templates/tasks-template.md
- Reviewed .specify/templates/commands/*.md (directory absent)
- Updated AGENTS.md
- Updated CLAUDE.md
- Added README.md, CONTRIBUTING.md, SECURITY.md, CODE_OF_CONDUCT.md, SUPPORT.md, CHANGELOG.md, and LICENSE
- Added docs/, checklists/, and GitHub governance templates
- Added docs/design-patterns.md and removed simplicity-first pattern language
Follow-up TODOs:
- None
-->

# PGX Constitution

## Core Principles

### I. Specification Is the Source of Truth

Every feature MUST begin with a specification that describes user goals, prioritized
user stories, functional requirements, assumptions, edge cases, and measurable
success criteria before implementation planning starts. Requirements MUST be written
in product language, not hidden inside implementation details. Any ambiguity that
affects scope, data, behavior, compliance, or user experience MUST be marked as
`NEEDS CLARIFICATION` until resolved.

Rationale: The specification is the contract that keeps implementation choices
anchored to user value and prevents undocumented scope changes.

### II. User-Story Slices Are Independently Valuable

User stories MUST be prioritized and structured so each P1/P2/P3 slice can be
implemented, tested, demonstrated, and shipped independently whenever practical.
The P1 story MUST define a usable MVP. Later stories MAY integrate with earlier
work, but they MUST NOT make the earlier delivered behavior untestable or dependent
on unfinished scope.

Rationale: Independent slices reduce delivery risk and create clear validation
checkpoints throughout the work.

### III. Verification Is Planned Before Implementation

Each feature MUST define how every user story, use case, key requirement, and
function-level behavior will be verified before implementation begins. Every
function introduced by implementation MUST have automated test coverage that
exercises its normal path, boundary or error path, or delegation contract. Trivial
framework hooks, generated glue, or declarations with no executable branch MAY be
covered through a higher-level component or integration test only when a direct unit
test would add no meaningful assertion. When automated tests are not practical for
a user-facing behavior, the plan or tasks MUST include explicit manual validation
steps with observable expected results. Tests MUST be written before the
implementation tasks they protect and MUST fail for the intended reason before
implementation proceeds.

Rationale: Verification discipline prevents tasks from becoming implementation-only
checklists with no reliable proof of behavior.

### IV. Plans Capture Technical Decisions

Implementation plans MUST record the chosen architecture, technology context,
project structure, constraints, dependencies, design patterns, and tradeoffs before
task generation. Each use case MUST name the design pattern or structure it uses
and explain why that choice fits the behavior, expected growth, extension points,
and test strategy. Any choice that expands scope, changes a contract, introduces a
new dependency, or applies a non-trivial design pattern MUST document the design
forces considered, the extension path it protects, and the operational risks.

Rationale: Design decisions need to be reviewable before they become scattered
across code and generated tasks.

### V. Traceability and Operational Clarity

Tasks MUST trace back to user stories, requirements, contracts, entities, or
cross-cutting concerns. Task descriptions MUST include exact file paths when files
are known. Plans and tasks MUST include logging, error handling, configuration,
security, and performance work when the feature affects runtime behavior or
operational risk.

Rationale: Traceability makes reviews, handoffs, and regressions easier to manage
without guessing why a change exists.

### VI. Clean Architecture Boundaries Are Mandatory

Application code MUST follow clean architecture dependency rules unless a documented
exception is approved in the plan. Domain entities and business rules MUST NOT
depend on UI, database, network, framework, or AI-provider code. Use cases MUST
orchestrate domain behavior through explicit input/output boundaries and ports.
Adapters MUST translate between external systems and application boundaries without
leaking provider-specific types into the domain. Framework code MUST remain at the
outer edge of the system.

Rationale: AI-generated code tends to couple quickly unless architectural boundaries
are explicit and testable.

## Delivery Constraints

Feature work MUST preserve the Spec Kit artifact flow:

1. `spec.md` defines user value, behavior, assumptions, and measurable outcomes.
2. `plan.md` defines technical context, structure, constitution checks, and
   complexity justifications.
3. Supporting design artifacts define research, data models, contracts, and
   quickstart validation when relevant.
4. `tasks.md` decomposes the plan into dependency-ordered, story-traceable work.

Generated artifacts MUST avoid unresolved placeholders unless they are explicitly
marked with `NEEDS CLARIFICATION` or a dated TODO that names the missing decision.
Agent-specific guidance MAY exist, but core project instructions MUST remain usable
by any supported Spec Kit integration.

## Development Workflow

The Constitution Check in every implementation plan MUST pass before Phase 0
research starts and MUST be rechecked after Phase 1 design. Reviews MUST confirm
that specifications, plans, and tasks remain aligned with this constitution before
implementation begins. If a feature violates a principle, the plan MUST document the
violation, the reason it is necessary, the extension path it protects, and the
tradeoffs accepted.

Implementation MUST proceed in dependency order: setup, foundational work, P1 MVP,
then later stories by priority unless parallel execution is explicitly safe. Each
completed story MUST be validated independently before depending work is treated as
complete.

## Governance

This constitution supersedes conflicting local conventions, generated templates, and
agent-specific instructions for feature specification, planning, task generation,
and implementation review.

Amendments MUST update this file and any dependent templates or guidance in the
same change. Every amendment MUST include a Sync Impact Report summarizing version
changes, principle changes, template updates, and deferred follow-up work.

Versioning follows semantic versioning:

- MAJOR: Backward-incompatible principle or governance changes, including removals
  or redefinitions of existing principles.
- MINOR: New principles, new governed sections, or materially expanded requirements.
- PATCH: Clarifications, wording fixes, template synchronization, or non-semantic
  refinements.

Compliance review is required during plan creation, after design artifacts are
produced, and before implementation is considered complete. Non-compliance MUST be
resolved or documented in the plan's Design Fit & Exception Tracking section.

**Version**: 1.1.0 | **Ratified**: 2026-05-05 | **Last Amended**: 2026-05-05
