# Current State: Customer Medallion Pipeline

## Purpose

This document describes what exists before the proposed medallion pipeline change.
It gives OpenSpec and AI coding agents enough context to avoid guessing about
existing systems, data structures, ownership, and constraints.

## Existing Source Systems

| System | Type | Owner | Current Role | Notes |
|---|---|---|---|---|
| `<fill in>` | Relational / Kafka / file / warehouse / other | `<fill in>` | `<fill in>` | `<fill in>` |

## Existing Databases, Topics, Files, Or Tables

| Asset | Type | Location | Update Pattern | Notes |
|---|---|---|---|---|
| `<fill in>` | Table / topic / file / API / other | `<fill in>` | Batch / streaming / CDC / manual / other | `<fill in>` |

## Current Source Structure

Document the current source structure here, or point to `SOURCE_CONTRACT.md` if
that file is the canonical source contract.

| Field | Type | Required | Sensitive | Notes |
|---|---|---:|---:|---|
| `<fill in>` | `<fill in>` | Yes / No | Yes / No | `<fill in>` |

## Existing Pipelines Or Jobs

| Pipeline Or Job | Schedule / Trigger | Owner | Current Behavior | Notes |
|---|---|---|---|---|
| `<fill in>` | `<fill in>` | `<fill in>` | `<fill in>` | `<fill in>` |

## Current Data Consumers

| Consumer | Use Case | Current Input | Pain Point |
|---|---|---|---|
| `<fill in>` | `<fill in>` | `<fill in>` | `<fill in>` |

## Current Problems

- `<fill in current pain point>`
- `<fill in current pain point>`
- `<fill in current pain point>`

## Known Constraints

- Spark and Spark SQL are required for transformation work.
- Source type must be clarified before proposal.
- Target type must be clarified before proposal.
- Real customer data must not be used in demos or tests.
- `<fill in additional constraint>`

## Open Questions

- Which source system is authoritative?
- Is ingestion batch, streaming, micro-batch, or CDC-based?
- Are existing consumers relying on the current structure?
- Are there existing quality issues that must be preserved, fixed, or rejected?
- Are there regulatory, retention, or lineage expectations?
