# Spec Kit Workflow

Spec Kit keeps AI-assisted development grounded in product intent, architecture,
and testable tasks.

## Artifact Flow

```text
idea -> spec.md -> clarification -> plan.md -> tasks.md -> analysis -> implementation
```

## 1. Specify

Create a feature specification from a natural-language idea.

The spec must define:

- User stories
- Priorities
- Acceptance scenarios
- Functional requirements
- Edge cases
- Assumptions
- Success criteria

## 2. Clarify

Resolve ambiguity before architecture or implementation.

Clarify at least:

- User roles
- Data ownership
- Privacy constraints
- AI automation limits
- Approval points
- Error handling
- Non-goals

## 3. Plan

The plan must define:

- Language and framework once chosen
- Clean architecture structure
- Use-case design patterns
- Ports and adapters
- Storage and external systems
- AI-provider boundaries
- Test strategy
- Complexity exceptions

## 4. Tasks

Tasks must be:

- Ordered by dependency
- Grouped by user story
- Independently testable
- Traceable to requirements
- Written with tests before implementation
- Specific about file paths when known

## 5. Analyze

Run consistency analysis before coding:

- Spec, plan, and tasks agree.
- Architecture rules are represented in tasks.
- Test coverage tasks exist for every behavior.
- No placeholders remain unresolved.

## 6. Implement

Implement in task order.

Do not skip tests. Do not bypass architecture boundaries. Do not add patterns that
were not justified in the plan.
