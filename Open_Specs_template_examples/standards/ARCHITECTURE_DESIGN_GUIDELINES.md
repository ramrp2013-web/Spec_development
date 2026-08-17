# Architecture And Design Guidelines

## Purpose

This document defines organization or team-level architecture and design
expectations. It should guide OpenSpec exploration, proposals, design documents,
implementation tasks, and code review.

It should not contain project-specific component names, schemas, file paths, or
business rules. Those belong in the change-specific context or the generated
OpenSpec change documents.

## Architecture Style

Each project or change should identify the intended architecture style.

Examples:

- Local batch pipeline.
- Backend API service.
- Frontend web application.
- Full-stack application.
- Event-driven service.
- Modular monolith.
- Microservice.

The selected style should be appropriate for the problem size and should avoid
unnecessary infrastructure or layers.

## System Boundaries

Every change should make ownership clear:

- What this system or change owns.
- What it does not own.
- Which external systems, files, APIs, or data sources it depends on.
- Which responsibilities are explicitly out of scope.

## Component Design

Components should have clear responsibilities.

Prefer:

- Small, focused modules.
- Clear entry points.
- Isolated core behavior.
- Shared helpers only when reuse is real.
- Tests that can exercise core behavior without unnecessary external dependencies.

Avoid:

- Broad utility modules with unrelated behavior.
- Hidden cross-module dependencies.
- New layers that do not reduce complexity.
- Components introduced only because they might be useful later.

## Dependency Direction

Projects should define allowed dependency direction.

General rule:

- Entry points may call application or pipeline logic.
- Application or pipeline logic may call configuration, domain, and helper modules.
- Core behavior should not depend on CLI, UI, test, or infrastructure-specific code.
- Tests may depend on implementation modules, but implementation modules must not depend on tests.

## Data Flow And Control Flow

Each change should describe the important flow in plain language or a simple diagram.

Examples:

- Request -> validation -> service logic -> persistence -> response.
- Source data -> validation -> transformation -> output -> verification.
- Event -> handler -> business rule -> side effect -> acknowledgement.

The flow should identify where validation, transformation, error handling, and output happen.

## Interfaces And Contracts

Changes must document relevant contracts.

Examples:

- API request and response contracts.
- File schemas.
- Table schemas.
- Event payloads.
- Function or module interfaces.
- Data quality expectations.

Project-specific contracts belong in the change-specific context, not in this standards file.

## Configuration Design

Configuration should be explicit and understandable.

Prefer:

- Clear names.
- Documented defaults.
- Small configuration surfaces.
- Environment-specific behavior only when needed.

Avoid:

- Hidden magic values.
- Complex configuration frameworks for simple projects.
- Hardcoded credentials or environment-specific paths.

## Error Handling Design

Errors should be clear, actionable, and appropriate to the system.

Projects should define expected behavior for:

- Missing inputs.
- Invalid configuration.
- Invalid data.
- Failed external dependencies.
- Failed writes or side effects.
- Partial completion.

Do not silently ignore failures that affect required behavior.

## Observability Design

Changes should define the observability level appropriate for the system.

Examples:

- Console output for a local learning demo.
- Structured logs for a service.
- Metrics and tracing for production systems.
- Audit logs for regulated workflows.

Avoid introducing external observability platforms unless they are in scope.

## Resilience And Recovery

Changes should state how the system behaves after failure.

Consider:

- Whether the operation is rerunnable.
- Whether partial output is allowed.
- Whether retries are needed.
- Whether failure state is inspectable.
- Whether cleanup is required.

## Performance And Scalability

Performance design should match the expected scale.

Changes should state:

- Expected data volume or traffic volume.
- Latency, throughput, or batch window expectations when relevant.
- Whether optimization is in scope.

Do not optimize for unconfirmed scale.

## Documentation Design

Documentation should explain:

- What the system or change does.
- How to run it locally.
- How to test it.
- Important contracts.
- Important tradeoffs.
- Operational notes when applicable.

## Notes For AI Agents

- Keep architecture proportional to the intent.
- Do not introduce new components, services, or patterns without a clear reason.
- Use the change-specific context for project details.
- Ask clarification questions when ownership, flow, contracts, or tradeoffs are unclear.
- Explain major design tradeoffs in the generated OpenSpec `design.md`.
