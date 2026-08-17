# Pipeline Design: Customer Medallion Pipeline

## Purpose

This document captures the intended medallion pipeline design before OpenSpec
generates the formal `design.md`. It controls the pipeline shape, layer
responsibilities, code structure, data quality approach, and design questions
that must be resolved before implementation.

## Pipeline Flow

```text
Source
  -> Landing / Raw
  -> Bronze
  -> Silver
  -> Gold
  -> Data Mart
```

## Processing Platform

The pipeline must use:

- Apache Spark.
- PySpark.
- Spark SQL.

Spark SQL must be used for transformation work in Bronze, Silver, Gold, or Data
Mart steps where records are selected, shaped, filtered, joined, aggregated, or
projected.

## Source

The source is selected during explore.

Supported source options:

- Relational database table.
- Kafka topic.
- File source such as CSV, JSON, or Parquet.
- Warehouse table.

Source details to clarify:

| Item | Value |
|---|---|
| Source type | `<fill in>` |
| Source system | `<fill in>` |
| Source object | `<fill in: table, topic, path, or warehouse object>` |
| Read mode | `<fill in: batch, streaming, micro-batch, CDC, full load, incremental>` |
| Incremental strategy | `<fill in: timestamp, offset, CDC marker, full refresh, other>` |
| Expected volume | `<fill in>` |

## Landing / Raw

Purpose:

```text
Capture source records as received.
```

Storage:

```text
<fill in: local path, ADLS path, Delta table, warehouse table, other>
```

Rules:

- Preserve source shape as much as practical.
- Add ingestion metadata when appropriate.
- Avoid business transformations.
- Keep enough lineage to replay or audit ingestion.
- Do not drop sensitive fields at this layer unless required by policy.

Typical metadata:

- `ingestion_timestamp`
- `source_system`
- `source_object`
- `batch_id`
- `record_hash`

## Bronze

Purpose:

```text
Standardize raw records for processing.
```

Storage:

```text
<fill in>
```

Rules:

- Parse and normalize technical schema details.
- Validate required fields exist.
- Add or preserve lineage columns from Landing / Raw.
- Track malformed or rejected records according to the selected error strategy.
- Avoid business-level enrichment unless explicitly approved.

## Silver

Purpose:

```text
Create cleaned and conformed customer records.
```

Storage:

```text
<fill in>
```

Rules:

- Use Spark SQL.
- Drop sensitive or internal fields.
- Keep approved analytical fields.
- Standardize field names and data types.
- Apply selected data quality rules.
- Preserve row count unless filtering or deduplication is selected.

Fields to drop in this example:

- `phone`
- `address`
- `internal_notes`

Expected Silver fields:

- `customer_id`
- `customer_name`
- `email`
- `signup_date`
- `status`

## Gold

Purpose:

```text
Create business-ready customer records.
```

Storage:

```text
<fill in>
```

Rules:

- Apply business-level naming and quality expectations.
- Include only approved consumer-safe fields.
- Document whether Gold is identical to Silver in version 1.
- Document any aggregations, derived fields, or business filters if they are selected.

## Data Mart

Purpose:

```text
Expose final customer data for consumption.
```

Target options:

- Local file.
- ADLS path.
- Relational table.
- Warehouse table.
- Data mart schema or serving table.

Target:

```text
<fill in>
```

Write mode:

```text
<fill in: overwrite, append, merge/upsert>
```

Rules:

- Write from Gold.
- Match the approved Data Mart contract.
- Document overwrite, partitioning, and access behavior.
- Document the expected consumer or consumer group.

## Proposed Code Structure

```text
src/
  config/
    settings.py

  ingestion/
    readers/
      relational_reader.py
      kafka_reader.py
      file_reader.py

  layers/
    landing_raw.py
    bronze.py
    silver.py
    gold.py
    data_mart.py

  quality/
    validators.py
    rejected_records.py

  contracts/
    customer_source_contract.py
    customer_layer_contracts.py

  utils/
    spark.py
    logging.py

tests/
  unit/
    test_silver_transform.py
    test_quality_rules.py

  integration/
    test_medallion_flow.py

  fixtures/
    customer_source_sample.csv

docs/
  runbook.md
```

## Code Structure Rules

- Put source-specific reading logic under `src/ingestion/readers/`.
- Put medallion layer transformations under `src/layers/`.
- Put data quality checks under `src/quality/`.
- Put source and layer contract definitions under `src/contracts/`.
- Put Spark session setup under `src/utils/spark.py`.
- Do not put source connection logic inside medallion layer files.
- Do not put medallion transformation logic inside source readers.
- Do not create new top-level folders without updating this design.

## Layer Contracts

Each layer must document:

- Input source.
- Output target.
- Required fields.
- Dropped or masked fields.
- Data quality rules.
- Error handling behavior.
- Storage format and location.

| Layer | Input | Output | Contract Summary |
|---|---|---|---|
| Landing / Raw | Selected source | Raw storage | Source shape plus ingestion metadata |
| Bronze | Landing / Raw | Bronze storage | Parsed and technically standardized records |
| Silver | Bronze | Silver storage | Cleaned and conformed customer records |
| Gold | Silver | Gold storage | Business-ready customer records |
| Data Mart | Gold | Consumer target | Final consumer-ready structure |

## Data Quality Rules

Define behavior for:

| Rule | Expected Behavior |
|---|---|
| Missing required field | `<fill in>` |
| Null `customer_id` | `<fill in>` |
| Duplicate `customer_id` | `<fill in>` |
| Invalid `signup_date` | `<fill in>` |
| Unexpected `status` | `<fill in>` |
| Malformed record | `<fill in>` |

## Rejected Record Strategy

```text
<fill in: fail fast, quarantine path, rejected-record table, rejected Kafka topic, error report>
```

Rejected records should include enough context to debug:

- Source system.
- Source object.
- Batch id, offset, or watermark value.
- Rejection reason.
- Original record or approved safe subset of the record.

## Testing Strategy

Tests should verify:

- Source reader loads approved synthetic input.
- Landing / Raw preserves source shape as expected.
- Bronze validates required fields.
- Silver drops sensitive or internal fields.
- Gold produces business-ready records.
- Data Mart output matches the approved contract.
- Spark SQL is used for transformation work.
- Rejected records follow the selected strategy.

## Open Questions

- Which source type is selected?
- Is processing batch, streaming, micro-batch, or CDC?
- Where is Landing / Raw stored?
- Where are Bronze, Silver, and Gold stored?
- Is ADLS required?
- What is the Data Mart target?
- What write mode should be used?
- Should Gold differ from Silver in version 1?
- What metadata columns are required?
- What rejected-record strategy should be used?
- Should duplicates be rejected, deduplicated, or preserved?
