---

description: "Task list template for feature implementation"
---

# Tasks: [FEATURE NAME]

**Input**: Design documents from `/specs/[###-feature-name]/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Verification**: Tests are mandatory for AI-generated implementation work. Every
implemented function MUST have automated coverage for its normal path, boundary or
error path, or delegation contract. Trivial framework hooks or generated glue MAY
be covered by component/integration tests only when direct unit tests add no
meaningful assertion. Tests MUST be written before the implementation tasks they
protect and MUST fail for the intended reason first.

**Organization**: Tasks are grouped by user story to enable independent
implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions
- Every implementation task that creates or changes functions MUST have a matching
  earlier test task

## Path Conventions

- **Single project**: `src/domain/`, `src/application/`, `src/infrastructure/`,
  `src/interfaces/`, `tests/`
- **Web app**: `backend/src/domain/`, `backend/src/application/`,
  `backend/src/infrastructure/`, `backend/src/interfaces/`, `frontend/src/`
- **Mobile**: `api/src/`, `ios/src/` or `android/src/`
- Paths shown below assume a single clean architecture project; adjust based on
  `plan.md` structure

<!--
  ============================================================================
  IMPORTANT: The tasks below are SAMPLE TASKS for illustration purposes only.

  The /speckit-tasks command MUST replace these with actual tasks based on:
  - User stories from spec.md (with priorities P1, P2, P3...)
  - Feature requirements from plan.md
  - Clean architecture boundaries and use-case patterns from plan.md
  - Entities from data-model.md
  - Endpoints/contracts from contracts/
  - Function-level test strategy from plan.md and constitution checks

  Tasks MUST be organized by user story so each story can be:
  - Implemented independently
  - Tested independently
  - Delivered as an MVP increment

  DO NOT keep these sample tasks in the generated tasks.md file.
  ============================================================================
-->

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

- [ ] T001 Create clean architecture project structure per implementation plan
- [ ] T002 Initialize [language] project with [framework] dependencies
- [ ] T003 [P] Configure linting, formatting, and type/static analysis tools
- [ ] T004 [P] Configure test runner with coverage thresholds
- [ ] T005 [P] Add architecture boundary test tooling or import-rule checks

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**CRITICAL**: No user story work can begin until this phase is complete

Examples of foundational tasks (adjust based on your project):

- [ ] T006 Define domain entities/value objects in `src/domain/`
- [ ] T007 Define application use-case interfaces and ports in `src/application/`
- [ ] T008 [P] Define adapter interfaces for persistence, AI providers, network, or external services
- [ ] T009 [P] Configure dependency-rule tests proving domain/application do not depend on infrastructure/interfaces
- [ ] T010 Configure error handling and logging boundaries
- [ ] T011 Setup environment configuration management

**Checkpoint**: Foundation ready; user story implementation can now begin in parallel

---

## Phase 3: User Story 1 - [Title] (Priority: P1) MVP

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### Tests for User Story 1 (MANDATORY)

> **NOTE: Write these tests FIRST, ensure they FAIL before implementation**

- [ ] T012 [P] [US1] Unit tests for [domain function/entity behavior] in `tests/unit/domain/[test_file]`
- [ ] T013 [P] [US1] Unit tests for [use-case function] in `tests/unit/application/[test_file]`
- [ ] T014 [P] [US1] Contract test for [port/endpoint] in `tests/contract/[test_file]`
- [ ] T015 [US1] Integration or component test for [user journey] in `tests/integration/[test_file]`

### Implementation for User Story 1

- [ ] T016 [P] [US1] Implement [Entity/ValueObject] in `src/domain/[entity_file]`
- [ ] T017 [P] [US1] Implement [UseCase/Interactor] in `src/application/[use_case_file]`
- [ ] T018 [US1] Implement [Port] in `src/application/ports/[port_file]`
- [ ] T019 [US1] Implement [Adapter] in `src/infrastructure/[adapter_file]`
- [ ] T020 [US1] Implement [Controller/Presenter/CLI] in `src/interfaces/[entrypoint_file]`
- [ ] T021 [US1] Add validation and error handling
- [ ] T022 [US1] Add logging for user story 1 operations

**Checkpoint**: User Story 1 is fully functional, independently testable, and covered by function-level tests

---

## Phase 4: User Story 2 - [Title] (Priority: P2)

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### Tests for User Story 2 (MANDATORY)

- [ ] T023 [P] [US2] Unit tests for [domain/application function] in `tests/unit/[layer]/[test_file]`
- [ ] T024 [P] [US2] Contract test for [port/endpoint] in `tests/contract/[test_file]`
- [ ] T025 [US2] Integration or component test for [user journey] in `tests/integration/[test_file]`

### Implementation for User Story 2

- [ ] T026 [P] [US2] Implement [Entity/ValueObject] in `src/domain/[entity_file]`
- [ ] T027 [US2] Implement [UseCase/Interactor] in `src/application/[use_case_file]`
- [ ] T028 [US2] Implement [Adapter/Controller] in `src/[layer]/[source_file]`
- [ ] T029 [US2] Integrate with User Story 1 components without breaking independent testability

**Checkpoint**: User Stories 1 and 2 both work independently and pass all tests

---

## Phase 5: User Story 3 - [Title] (Priority: P3)

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### Tests for User Story 3 (MANDATORY)

- [ ] T030 [P] [US3] Unit tests for [domain/application function] in `tests/unit/[layer]/[test_file]`
- [ ] T031 [P] [US3] Contract test for [port/endpoint] in `tests/contract/[test_file]`
- [ ] T032 [US3] Integration or component test for [user journey] in `tests/integration/[test_file]`

### Implementation for User Story 3

- [ ] T033 [P] [US3] Implement [Entity/ValueObject] in `src/domain/[entity_file]`
- [ ] T034 [US3] Implement [UseCase/Interactor] in `src/application/[use_case_file]`
- [ ] T035 [US3] Implement [Adapter/Controller] in `src/[layer]/[source_file]`

**Checkpoint**: All user stories are independently functional and covered by tests

---

[Add more user story phases as needed, following the same pattern]

---

## Phase N: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

- [ ] TXXX [P] Documentation updates in docs/
- [ ] TXXX Code cleanup and refactoring without crossing architecture boundaries
- [ ] TXXX Performance optimization across all stories
- [ ] TXXX [P] Additional unit tests for uncovered functions in `tests/unit/`
- [ ] TXXX [P] Architecture boundary tests in `tests/architecture/`
- [ ] TXXX Security hardening
- [ ] TXXX Run quickstart.md validation
- [ ] TXXX Manual validation for scenarios that cannot be automated, with expected results

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies; can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion; BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel if they touch different files
  - Or sequentially in priority order (P1 -> P2 -> P3)
- **Polish (Final Phase)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational; no dependencies on other stories
- **User Story 2 (P2)**: Can start after Foundational; may integrate with US1 but remains independently testable
- **User Story 3 (P3)**: Can start after Foundational; may integrate with US1/US2 but remains independently testable

### Within Each User Story

- Tests MUST be written and FAIL before implementation
- Each implementation function MUST have a matching automated test path
- Domain models before application use cases
- Application ports before infrastructure adapters
- Use cases before interface controllers/presenters
- Core implementation before integration
- Story complete before moving to next priority

### Parallel Opportunities

- Setup tasks marked [P] can run in parallel
- Foundational tasks marked [P] can run in parallel within Phase 2
- Tests for a user story marked [P] can run in parallel
- Domain models and independent use cases marked [P] can run in parallel
- Different user stories can be worked on in parallel only when file ownership does not conflict

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational
3. Write failing tests for User Story 1
4. Complete Phase 3: User Story 1 implementation
5. STOP and VALIDATE: Run unit, contract, integration, and architecture tests
6. Deploy/demo only if all gates pass

### Incremental Delivery

1. Complete Setup + Foundational -> foundation ready
2. Add User Story 1 -> test independently -> deploy/demo
3. Add User Story 2 -> test independently -> deploy/demo
4. Add User Story 3 -> test independently -> deploy/demo
5. Each story adds value without breaking previous stories

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to a user story for traceability
- Every function must be covered by automated tests before deployment
- Verify tests fail before implementing
- Commit after each task or logical group
- Stop at checkpoints to validate independently
- Avoid: vague tasks, same-file conflicts, cross-story dependencies that break independence, and patterns without a use-case rationale
