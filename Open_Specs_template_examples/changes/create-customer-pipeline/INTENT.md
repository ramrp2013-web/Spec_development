# Intent: Create Customer Medallion Pipeline

## Problem

Build a Spark data engineering pipeline that ingests customer records from an
approved source and processes them through a medallion architecture:

```text
Source -> Landing / Raw -> Bronze -> Silver -> Gold -> Data Mart
```

The pipeline must use Spark and Spark SQL for transformation work. The source may
be relational, streaming, file-based, or another approved enterprise source. The
target may be local storage, cloud storage such as ADLS, a warehouse, or a data
mart target, depending on what is clarified during explore.

## Goal

Create a medallion architecture example that demonstrates how OpenSpec can guide
a data engineering change from intent through proposal, specification, design,
tasks, implementation, validation, and archive.

The example should show how raw source data becomes progressively more trusted,
curated, and business-ready across medallion layers.

## Audience

- Data engineers implementing medallion pipelines.
- Engineers learning OpenSpec.
- Teams standardizing AI-assisted data engineering workflows.
- Reviewers who need a consistent way to inspect source, layer, contract, and quality decisions.

## Source

The source contains synthetic customer records.

Source type options include:

- Relational source, such as an operational database table.
- Streaming source, such as Kafka.
- File source, such as CSV, JSON, or Parquet.
- Warehouse source, such as an existing analytics table.

The selected source type, connection approach, source location, access method,
read mode, and expected volume must be clarified before proposal.

Expected source fields for this customer example:

- `customer_id`
- `customer_name`
- `email`
- `phone`
- `address`
- `signup_date`
- `status`
- `internal_notes`

## Medallion Flow

The pipeline should follow this flow:

```text
Source
  -> Landing / Raw
  -> Bronze
  -> Silver
  -> Gold
  -> Data Mart
```

## Landing / Raw Layer

The Landing / Raw layer captures source data as received.

Expected behavior:

- Ingest records from the selected source.
- Preserve the original source shape as much as practical.
- Add ingestion metadata when appropriate, such as load timestamp, source name, or batch identifier.
- Avoid business transformations in this layer.
- Make the raw ingestion auditable and replayable when practical.

## Bronze Layer

The Bronze layer standardizes raw records for processing.

Expected behavior:

- Apply technical parsing and schema normalization.
- Validate required fields exist.
- Track malformed or rejected records according to the clarified error strategy.
- Preserve enough lineage to trace records back to Landing / Raw.
- Avoid business-level enrichment unless explicitly approved.

## Silver Layer

The Silver layer produces cleaned and conformed customer records.

Expected behavior:

- Use Spark SQL for transformation logic.
- Keep approved analytical fields.
- Drop sensitive or internal fields that should not flow downstream.
- Standardize field names and data types where required.
- Preserve row count unless filtering or deduplication is explicitly selected.

Fields to drop in this example:

- `phone`
- `address`
- `internal_notes`

Expected Silver output fields:

- `customer_id`
- `customer_name`
- `email`
- `signup_date`
- `status`

## Gold Layer

The Gold layer prepares business-ready data.

Expected behavior:

- Produce a curated customer dataset suitable for downstream analytics.
- Apply business-level naming, ordering, and quality expectations.
- Include only fields approved for consumption.
- Document whether Gold is identical to Silver for the first version or adds additional business shaping.

## Data Mart

The Data Mart layer exposes the final consumer-ready structure.

Target options include:

- Local file output for learning or development.
- ADLS or another approved cloud storage location.
- Relational table.
- Warehouse table.
- Data mart schema or serving table.

The selected Data Mart target, write mode, partitioning strategy, overwrite
behavior, and access pattern must be clarified before proposal.

## Data Quality Expectations

The pipeline should define behavior for:

- Missing required source fields.
- Malformed records.
- Duplicate customer identifiers.
- Null customer identifiers.
- Invalid signup dates.
- Unexpected status values.
- Rejected record handling.

The first version may keep these rules simple, but the expected behavior must be
clear before implementation.

## Success Summary

The project is successful when the pipeline can read from the selected source,
process records through Landing / Raw, Bronze, Silver, Gold, and Data Mart layers,
use Spark SQL for transformations, drop selected sensitive or internal fields,
write the selected Data Mart target, and pass the required tests.

## Explore Instructions

Before creating an OpenSpec proposal, clarify:

- Source type: relational, Kafka, file, warehouse, or other.
- Source read mode: batch, streaming, or micro-batch.
- Landing / Raw storage format and location.
- Bronze, Silver, Gold, and Data Mart storage formats and locations.
- Whether ADLS or another cloud target is required.
- Whether Gold differs from Silver in version 1.
- Data Mart target type and write mode.
- Required metadata columns.
- Schema strategy.
- Error and rejected-record strategy.
- Deduplication expectations.
- Data quality rules.
- Test depth and required fixtures.
