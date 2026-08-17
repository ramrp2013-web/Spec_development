# Intent: Create Customer Pipeline

## Problem

Build a small data engineering pipeline that reads a source CSV file containing
customer records, transforms the data using Spark SQL, drops selected fields, and
writes the transformed result as a CSV file.

## Goal

Create a local PySpark and Spark SQL example that demonstrates how OpenSpec can
guide a data engineering change from intent through proposal, specification,
design, tasks, implementation, and verification.

## Audience

- Engineers learning OpenSpec.
- Data engineers learning spec-driven development.
- Teams standardizing AI-assisted development workflows.

## Source

The source data is a local CSV file with synthetic customer records.

Expected source columns:

- `customer_id`
- `customer_name`
- `email`
- `phone`
- `address`
- `signup_date`
- `status`
- `internal_notes`

## Transformation

The pipeline should use Spark SQL.

The pipeline should:

- Load the CSV into Spark.
- Register the source data as a temporary SQL view.
- Run a SQL `SELECT` statement that keeps approved columns.
- Drop `phone`, `address`, and `internal_notes`.

## Target

The transformed output should be written as a local CSV file.

Expected output columns:

- `customer_id`
- `customer_name`
- `email`
- `signup_date`
- `status`

## Success Summary

The project is successful when the pipeline can read local CSV input, transform it
using Spark SQL, drop selected fields, write local CSV output, and run locally with
tests.

## Explore Instructions

Before creating an OpenSpec proposal, clarify open questions about schema handling,
output overwrite behavior, test depth, output file format, and malformed records.
