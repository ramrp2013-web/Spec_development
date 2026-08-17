# Design Guidelines

## Purpose

This document defines design expectations for the CSV Spark SQL pipeline example.
It explains how the solution should be shaped once the intent and requirements are clear.

## Design Principles

- Keep the first version beginner-friendly.
- Make data flow easy to inspect.
- Prefer explicit transformation behavior over hidden magic.
- Use Spark SQL as the central transformation mechanism.
- Keep design choices proportional to the small local scope.

## Transformation Design

- Read the input CSV into a Spark DataFrame.
- Register the DataFrame as a temporary Spark SQL view.
- Use a SQL `SELECT` statement to choose approved output columns.
- Do not implement the core transformation using only DataFrame column selection.

## Data Contract Design

Use the change-specific context as the canonical source for:

- Expected source columns.
- Approved output columns.
- Dropped fields.
- Data quality rules.

Do not put project-specific schemas in this standards document. If the data
contract changes, update the change-specific context first and then update design
guidance only when the implementation approach changes.

## Configuration Design

- Keep column lists explicit.
- Keep local input and output paths visible.
- Prefer simple constants or simple configuration structures for this example.
- Do not add a complex configuration framework.

## File Output Design

- Write output as CSV.
- Include headers.
- Preserve all rows unless filtering is explicitly introduced later.
- Document whether output is written as a Spark output directory or a single file.

## Error Design

- Error messages should help the learner understand what failed.
- Missing input and missing columns should be clear failures.
- Avoid swallowing Spark exceptions without useful context.

## Documentation Design

Documentation should explain:

- What the pipeline does.
- How to install dependencies.
- How to run the pipeline.
- How to run tests.
- Which columns are kept and dropped.

## Notes For AI Agents

- Use simple, readable design.
- Explain tradeoffs in `design.md` when OpenSpec generates the change.
- Ask before changing major design choices such as schema inference, output mode,
  or single-file output.
