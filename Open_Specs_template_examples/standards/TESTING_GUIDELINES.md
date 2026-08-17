# Testing Guidelines

## Purpose

This document defines testing expectations for the CSV Spark SQL pipeline example.
Tests should prove the required behavior without making the learning project heavy.

## Test Framework

- Use pytest.
- Use small synthetic sample data.
- Tests should run locally.

## Required Test Coverage

Tests should verify:

- The pipeline can read expected CSV input.
- Required source columns are present.
- Spark SQL transformation removes dropped fields.
- Expected output columns are retained.
- Row count is preserved.
- Output CSV is written successfully.
- Missing input or invalid schema fails clearly where practical.

## Test Data

- Use synthetic customer records only.
- Keep data small enough to inspect manually.
- Do not use real personal data.

## Unit Tests

Unit tests should cover:

- Column selection behavior.
- Configuration values.
- Helper functions.
- Validation logic.

## Integration Tests

At least one test should run the pipeline against a small local input and verify
the produced output shape.

## Assertions

Prefer assertions that check business behavior:

- Output contains approved columns.
- Output does not contain dropped columns.
- Output row count matches input row count.

Avoid assertions that depend on incidental Spark internals.

## Performance Tests

No performance tests are required for the first version.

## Notes For AI Agents

- Add or update tests when behavior changes.
- Do not mark tasks complete until relevant tests pass.
- If Spark cannot run in the current environment, report the limitation clearly.
