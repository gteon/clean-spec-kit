# Design Pattern Catalog

This starter is fit-first. Agents must choose the pattern that best fits the use
case, domain behavior, expected growth, extension points, test strategy, and clean
architecture boundaries.

The right pattern may create more files than a direct implementation. That is
acceptable when it makes future additions safer and easier to test.

## Pattern Decision Criteria

Choose patterns by asking:

- What behavior is being modeled?
- What is likely to grow: rules, providers, screens, steps, states, or workflows?
- Where are the extension points?
- What needs isolated tests?
- Which clean architecture boundary must be protected?
- What tradeoffs does the pattern introduce?

## Common Patterns

| Pattern | Use When | Extension Benefit | Test Benefit |
|---------|----------|-------------------|--------------|
| Use Case / Interactor | A user or system workflow coordinates domain behavior | New workflows get separate orchestration units | Use cases can be tested with fake ports |
| Port and Adapter | Code depends on a database, API, AI provider, file system, clock, queue, or network | Swap providers without changing domain/application | Adapters can be contract-tested |
| Repository | Retrieval/storage of aggregates or entities must hide persistence details | Persistence strategy can change behind a stable port | Use cases test against fake repositories |
| Specification | Business rules must be reused, combined, enabled, disabled, or expanded | Add rules without editing a central conditional block | Each rule/specification is independently tested |
| Composite | Rules, permissions, menus, screens, or structures form trees | Add nested behavior through composition | Leaf and composite behavior can be tested separately |
| Pipeline | Data passes through ordered validation, enrichment, parsing, or AI-output stages | Add, remove, or reorder stages without rewriting the flow | Each stage and the full pipeline are testable |
| Chain of Responsibility | Multiple handlers may process, reject, transform, or fall back | Add handlers without changing existing handlers | Handler order and fallback behavior are testable |
| Strategy | Algorithms, ranking, pricing, prompts, provider policies, or decisions vary | Add strategies without changing callers | Each strategy is tested behind the same contract |
| Command | Actions need validation, authorization, queueing, retry, undo, audit, or replay | Add command handlers and middleware around actions | Commands are tested as behavior units |
| Builder | Constructing an object requires ordered steps, optional parts, or valid combinations | Add construction options without telescoping constructors | Valid and invalid build paths are testable |
| Factory | Object creation is conditional, centralized, or hides implementation details | Add implementations without spreading conditionals | Creation choices are testable in one place |
| Abstract Factory | Related families of providers, adapters, or components must be created together | Add a provider family without changing use cases | Provider families are tested through shared contracts |
| Decorator | Logging, caching, retries, metrics, authorization, or tracing wraps behavior | Add cross-cutting behavior without editing core logic | Decorators can be tested around fake components |
| Facade | Multiple subsystems need one stable API | Internal subsystem changes do not affect callers | Facade behavior is tested at the boundary |
| Observer / Event Publisher | Independent subscribers react to domain or application events | Add subscribers without changing publishers | Event publication and handlers are tested separately |
| State | Behavior changes by lifecycle state | Add or change states without large conditionals | Each state transition is testable |
| Presenter / ViewModel | UI formatting must stay out of domain and use cases | Add screens/components without duplicating formatting | Presentation mapping is testable without UI rendering |
| Policy Object | Authorization, eligibility, limits, or business policy must be explicit | Add policy variants without changing workflows | Policies are tested with focused scenarios |

## Example: Rules That May Grow

If there are 5 validation rules today and likely 50 tomorrow, do not centralize
them in one large conditional function. Prefer one of:

- Specification: each rule is a composable object.
- Composite: rules can be grouped into nested rule sets.
- Pipeline: rules execute as ordered stages.
- Chain of Responsibility: handlers decide whether they can process or pass on.
- Policy Object: business policy is explicit and replaceable.

The plan must explain which one fits the domain and why.

## Example: AI Output Processing

AI output commonly needs parsing, validation, normalization, safety checks,
scoring, and persistence. Good candidates:

- Pipeline for ordered processing stages.
- Strategy for provider-specific parsing or scoring behavior.
- Adapter for provider SDK isolation.
- Specification or Policy Object for safety and business-rule checks.
- Decorator for retries, logging, metrics, and tracing.

Do not place provider SDK types or prompt formats in domain code.

## Example: Reusable Screens

When a new screen is needed:

- Use case/interactor coordinates behavior.
- Presenter/view model prepares display data.
- Composite can model nested component trees or menus.
- Strategy can swap layout or rendering policies.
- Builder can assemble complex screen configuration.
- Observer/Event Publisher can update independent UI areas after domain events.

New screens should compose stable components instead of duplicating behavior.
