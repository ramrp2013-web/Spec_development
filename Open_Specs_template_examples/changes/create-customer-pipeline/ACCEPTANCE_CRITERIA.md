# Acceptance Criteria: Create Customer Pipeline

## Functional Acceptance Criteria

- The pipeline reads customer records from a local CSV file.
- The pipeline uses PySpark.
- The pipeline uses Spark SQL for the transformation.
- The pipeline creates a temporary SQL view before running the transformation query.
- The pipeline removes `phone`, `address`, and `internal_notes` from output.
- The pipeline keeps `customer_id`, `customer_name`, `email`, `signup_date`, and `status`.
- The pipeline writes transformed data as CSV.
- The pipeline can run locally.

## Data Acceptance Criteria

- Input data is synthetic.
- Output contains only approved output columns.
- Output excludes all dropped fields.
- Output preserves input row count.
- Missing required source columns fail clearly.

## Testing Acceptance Criteria

- Tests verify the transformation removes dropped fields.
- Tests verify the transformation keeps expected output fields.
- Tests verify row count preservation.
- Tests verify the pipeline can run against small local sample data.
- Tests pass locally before the change is considered complete.

## Documentation Acceptance Criteria

- README explains setup.
- README explains how to run the pipeline.
- README explains how to run tests.
- Documentation identifies source columns, dropped columns, and output columns.

## OpenSpec Acceptance Criteria

- Proposal, spec, design, and tasks are generated before implementation.
- The generated spec describes behavior with requirements and scenarios.
- The implementation follows the approved tasks.
- Completed work is validated before archive.
