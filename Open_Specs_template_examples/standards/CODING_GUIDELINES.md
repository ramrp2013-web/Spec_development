# Coding Guidelines

## Purpose

This document defines organization or team-level coding expectations. AI coding
agents should follow these rules when implementing OpenSpec tasks.

It should not contain project-specific filenames, schemas, queries, or business rules.

## General Style

- Write readable code.
- Use meaningful function, class, module, and variable names.
- Keep functions focused.
- Prefer explicit behavior over clever behavior.
- Avoid unnecessary abstractions.
- Match existing project patterns before introducing new ones.

## Project Organization

Each project should define its expected folder and module structure in project
documentation or change-specific design.

General expectations:

- Keep entry points separate from core behavior.
- Keep configuration separate from business or transformation logic.
- Keep tests separate from implementation code.
- Keep reusable helpers focused and cohesive.

## Language Guidelines

Follow the conventions of the approved language and framework.

Examples:

- Use standard formatting tools when the project defines them.
- Use type hints or static types where they improve maintainability.
- Keep public interfaces stable and documented.
- Avoid broad exception handling that hides failures.

## Data Access Guidelines

When working with data sources:

- Use structured APIs or query tools appropriate to the source.
- For relational sources, use parameterized queries or approved query builders.
- For file sources, validate paths, formats, headers, and schema expectations.
- For APIs, validate request and response contracts.
- Do not hardcode credentials or environment-specific endpoints.

## Transformation Guidelines

- Keep transformation logic easy to inspect.
- Separate data reading, validation, transformation, and writing where practical.
- Treat data contracts as required behavior.
- Prefer deterministic transformations that can be tested with small fixtures.

## Error Handling

- Validate required inputs before processing.
- Raise or return clear errors for invalid inputs.
- Do not silently continue after failed reads, writes, external calls, or validations.
- Preserve useful context while avoiding sensitive data exposure.

## Logging

- Use the project-approved logging approach.
- Log major workflow steps when useful.
- Do not log secrets or sensitive values.
- Avoid adding external logging dependencies unless approved.

## Comments

- Add comments only when they clarify non-obvious behavior.
- Do not comment every line.
- Prefer readable names and small functions over explanatory comments.

## Documentation In Code

- Public functions, classes, endpoints, or modules should have concise documentation when useful.
- Keep usage examples in project documentation unless inline examples are a local convention.

## Notes For AI Agents

- Match the existing codebase style.
- Keep edits scoped to the requested change.
- Do not add new dependencies unless required by the OpenSpec change and approved by platform standards.
- Ask before changing project structure, public interfaces, or data access patterns.
