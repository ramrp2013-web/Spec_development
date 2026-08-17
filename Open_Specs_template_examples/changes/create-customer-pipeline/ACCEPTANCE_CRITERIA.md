# Acceptance Criteria: Create Customer Medallion Pipeline

## Functional Acceptance Criteria

- The selected source type is documented before implementation.
- The selected target type is documented before implementation.
- The pipeline uses Spark through PySpark.
- The pipeline uses Spark SQL for transformation work.
- The pipeline ingests customer records into a Landing / Raw layer.
- The pipeline creates a Bronze layer from Landing / Raw data.
- The pipeline creates a Silver layer from Bronze data.
- The pipeline creates a Gold layer from Silver data.
- The pipeline writes a Data Mart output from Gold data.
- Each medallion layer has a documented purpose, storage location, and data contract.
- The Silver or downstream layer removes `phone`, `address`, and `internal_notes`.
- The approved downstream fields include `customer_id`, `customer_name`, `email`, `signup_date`, and `status`.
- The pipeline can run in the approved runtime environment.

## Data Acceptance Criteria

- Input data is synthetic unless explicitly approved otherwise.
- Landing / Raw preserves source data shape as much as practical.
- Bronze validates required fields and standardizes technical schema details.
- Silver contains cleaned and conformed customer records.
- Gold contains business-ready customer records.
- Data Mart contains consumer-ready customer records.
- Output excludes all fields marked for dropping.
- Row count is preserved unless filtering or deduplication is explicitly selected.
- Missing required source fields fail clearly or are routed to a documented rejected-record path.

## Testing Acceptance Criteria

- Tests verify records can move through each medallion layer.
- Tests verify Spark SQL is used for transformation work.
- Tests verify dropped fields do not appear in Silver, Gold, or Data Mart outputs.
- Tests verify expected downstream fields are present.
- Tests verify row count preservation or the selected filtering/deduplication behavior.
- Tests verify malformed or invalid records follow the documented error strategy.
- Tests use approved synthetic test data.
- Tests pass before the change is considered complete.

## Documentation Acceptance Criteria

- Documentation identifies source type, read mode, and access method.
- Documentation identifies each medallion layer and its purpose.
- Documentation identifies storage format and location for each layer.
- Documentation identifies source fields, dropped fields, downstream fields, and Data Mart output.
- Documentation explains setup, execution, testing, and validation.

## OpenSpec Acceptance Criteria

- Proposal, spec, design, and tasks are generated before implementation.
- The generated spec describes medallion-layer behavior with requirements and scenarios.
- The generated design explains source ingestion, layer transitions, Spark SQL transformations, and target writes.
- The implementation follows the approved tasks.
- Completed work is validated before archive.
