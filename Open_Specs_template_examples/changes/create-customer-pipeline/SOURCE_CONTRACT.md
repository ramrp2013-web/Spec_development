# Source Contract: Customer Records

## Purpose

This document defines the source data contract for the customer medallion pipeline.
It is change-specific and may contain actual source structures, field names, data
types, sensitivity flags, and read behavior.

## Source Type

Select and document the source type during explore.

```text
<fill in: relational table, Kafka topic, file, warehouse table, API, other>
```

## Source Location

Document the source location or approved alias.

```text
<fill in: database/schema/table, topic name, path, endpoint, catalog reference>
```

## Read Mode

```text
<fill in: batch, streaming, micro-batch, CDC, full load, incremental>
```

## Source Owner

```text
<fill in source owner or owning team>
```

## Source Schema

| Field | Type | Required | Sensitive | Description |
|---|---|---:|---:|---|
| `customer_id` | string | Yes | No | Unique customer identifier |
| `customer_name` | string | Yes | No | Customer display name |
| `email` | string | Yes | No | Customer email address |
| `phone` | string | No | Yes | Customer phone number |
| `address` | string | No | Yes | Customer address |
| `signup_date` | date | No | No | Date the customer signed up |
| `status` | string | Yes | No | Customer status |
| `internal_notes` | string | No | Yes | Internal operational notes |

## Incremental Or Streaming Logic

Document how new or changed records are identified.

```text
<fill in: full refresh, updated_at watermark, CDC column, Kafka offset, event timestamp, etc.>
```

## Required Data Quality Rules

- `customer_id` must not be null.
- Required fields must exist before transformation.
- Malformed records must follow the rejected-record strategy.
- Sensitive fields must not flow to downstream consumer-ready layers unless explicitly approved.

## Rejected Record Strategy

```text
<fill in: fail fast, quarantine table/path, rejected-record topic, error report, etc.>
```

## Open Questions

- Is `email` approved for downstream analytical use?
- What values are valid for `status`?
- Should duplicate `customer_id` values be rejected, deduplicated, or preserved?
- Which timestamp or offset should drive incremental processing?
