# Architecture Guidelines

## Purpose

This document defines architecture expectations for the CSV Spark SQL pipeline
example. It should guide OpenSpec proposal, design, task, and implementation work.

## Architecture Style

Local batch data pipeline architecture.

## System Boundaries

This system owns:

- Reading local customer CSV input.
- Transforming customer data with Spark SQL.
- Dropping selected sensitive or internal fields.
- Writing transformed local CSV output.
- Verifying transformation behavior with tests.

This system does not own:

- Scheduling.
- Cloud storage.
- Database ingestion.
- Streaming.
- Production deployment.
- Real customer data management.

## Main Components

| Component | Responsibility | Notes |
|---|---|---|
| `src/config.py` | Stores paths, Spark settings, and column configuration | Keep simple and explicit |
| `src/pipeline.py` | Reads input, runs Spark SQL transformation, writes output | Core pipeline behavior |
| `src/utils.py` | Shared helpers for validation or filesystem behavior | Avoid broad utility sprawl |
| `tests/` | Verifies transformation and pipeline behavior | Use small synthetic data |
| `README.md` | Explains setup, execution, and verification | Beginner-friendly |

## Dependency Direction

- Entry points may call pipeline logic.
- Pipeline logic may use configuration and utility helpers.
- Utility helpers should not depend on pipeline orchestration.
- Tests may import configuration, utilities, and pipeline functions.

## Data Flow

```text
local CSV input
  -> Spark DataFrame
  -> temporary Spark SQL view
  -> Spark SQL SELECT query
  -> transformed DataFrame
  -> local CSV output
```

## Interfaces And Contracts

- Input CSV must contain the expected source columns.
- Output CSV must contain only approved output columns.
- Dropped columns must not appear in output.
- Row count should be preserved unless a future requirement introduces filtering.

## Configuration Strategy

- Use simple project configuration for the first version.
- Keep input path, output path, Spark app name, columns to keep, and columns to drop visible.
- Avoid environment-specific configuration systems unless explicitly requested.

## Error Handling Strategy

- Fail clearly when the input file is missing.
- Fail clearly when required columns are missing.
- Fail clearly when Spark cannot read or write data.
- Do not silently ignore invalid input or incomplete output.

## Observability Architecture

- Basic logs or clear console messages are enough for the first version.
- No external observability platform is required.

## Scalability And Performance

- Optimize for clarity, not large-scale performance.
- Use small local sample data.
- Do not add partitioning, caching, or tuning unless a later change requires it.

## Resilience And Recovery

- The pipeline should be rerunnable locally.
- Source data must not be modified.
- Partial output behavior should be documented if overwrite mode is used.

## Testing Architecture

- Core transformation logic must be testable with pytest.
- Tests should use synthetic sample data.
- Tests should verify output columns and row count.

## Out Of Bounds

- No new services.
- No new databases.
- No scheduler.
- No streaming architecture.
- No production deployment architecture.

## Notes For AI Agents

- Keep the architecture simple and local.
- Prefer direct modules over unnecessary layers.
- Do not introduce components that are not required by the intent.
