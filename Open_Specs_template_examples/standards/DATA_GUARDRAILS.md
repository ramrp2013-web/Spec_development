# Data Guardrails

## Purpose

This document defines organization or team-level data handling expectations.
It should not contain project-specific schemas, field names, tables, files, or
business data structures.

Change-specific data contracts belong in the change context, such as:

- `changes/<change-name>/INTENT.md`
- `changes/<change-name>/ACCEPTANCE_CRITERIA.md`
- A dedicated `changes/<change-name>/DATA_CONTRACT.md` when the contract is large

## Source Data Rules

- Every change that reads data must identify its source data.
- Every change must state whether source data is synthetic, masked, or production data.
- Sample data used for tests or demos must be synthetic unless explicitly approved.
- Source files, tables, APIs, or events must be documented in the change-specific context.

## Output Data Rules

- Every change that writes data must identify its output location, format, and contract.
- Output data must not include fields that the change marks as sensitive, internal, or out of scope.
- Output behavior must be clear when output already exists.
- Changes must state whether row count should be preserved, reduced, or expanded.

## Data Contract Rules

Change-specific context must define:

- Required source fields.
- Optional source fields, if any.
- Approved output fields.
- Dropped, masked, or transformed fields.
- Required data formats.
- Any row-level filtering or aggregation behavior.

## Data Quality Rules

Changes should define expected behavior for:

- Missing source data.
- Missing required fields.
- Malformed records.
- Duplicate records.
- Null or empty values.
- Invalid data types.
- Unexpected extra fields.

## Schema Rules

- The schema strategy must be explicit in the change-specific context or OpenSpec design.
- Schema inference is allowed only when the change accepts its tradeoffs.
- Explicit schemas are preferred when stable data contracts matter.

## PII And Sensitive Data Rules

- Do not use real personal data in demos, tests, or examples.
- Sensitive fields must be identified in the change-specific data contract.
- Sensitive fields must not be logged, written to unsafe outputs, or included accidentally.
- Masking, dropping, or tokenization decisions must be documented.

## Notes For AI Agents

- Do not invent data contracts.
- Read the change-specific context for actual source and output structures.
- Ask clarification questions when source fields, output fields, or sensitive fields are unclear.
- Treat data contracts as required behavior, not implementation detail.
