# Testing Guidelines

## Purpose

This document defines organization or team-level testing expectations. Tests should
prove required behavior without making the project unnecessarily heavy.

It should not contain project-specific schemas, filenames, tables, or field names.

## Test Framework

Use the test framework approved in `TECH_PLATFORM.md`.

Examples:

- pytest.
- unittest.
- Jest.
- Playwright.
- JUnit.
- dbt tests.

## Required Test Coverage

Each change should define tests for:

- Required behavior.
- Important edge cases.
- Error handling.
- Data contracts or API contracts.
- Security or privacy behavior when relevant.

## Test Data

- Use synthetic or approved masked data.
- Keep fixtures small enough to inspect.
- Do not use real personal data in tests or examples.
- For relational sources, use approved test databases, containers, schemas, or mocks.
- For file sources, use small fixture files.
- For APIs, use contract fixtures or approved mocks.

## Unit Tests

Unit tests should cover isolated behavior such as:

- Validation logic.
- Transformation logic.
- Mapping logic.
- Error handling.
- Helper functions.

## Integration Tests

Integration tests should cover meaningful boundaries when practical.

Examples:

- Read from a fixture file and write an output artifact.
- Read from a test relational table and verify target table changes.
- Call a local test API and verify request/response behavior.
- Run a pipeline against synthetic data and verify output contract.

## Contract Tests

Use contract tests when a change depends on structured inputs or outputs.

Examples:

- Required source fields exist.
- Output fields match the approved contract.
- API response shape is stable.
- Relational table columns and types match expectations.

## Assertions

Prefer assertions that check required behavior:

- Expected records are produced.
- Expected fields are present.
- Forbidden fields are absent.
- Row counts, aggregate counts, or status values match expectations when relevant.
- Error cases fail clearly.

Avoid assertions that depend on incidental implementation details unless those details
are part of the requirement.

## Performance Tests

Performance tests are required only when the change defines performance, scale,
latency, throughput, or batch-window expectations.

## Notes For AI Agents

- Add or update tests when behavior changes.
- Do not mark tasks complete until relevant tests pass or an environment limitation is clearly reported.
- If required external systems are unavailable, use approved mocks or fixtures and document the limitation.
