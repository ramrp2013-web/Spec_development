# Coding Guidelines

## Purpose

This document defines coding expectations for the CSV Spark SQL pipeline example.
AI coding agents should follow these rules when implementing OpenSpec tasks.

## General Style

- Write readable Python.
- Use meaningful function and variable names.
- Keep functions focused.
- Avoid unnecessary abstractions.
- Prefer explicit code over clever code.

## Project Organization

- Put pipeline behavior in `src/pipeline.py`.
- Put configuration in `src/config.py`.
- Put small reusable helpers in `src/utils.py`.
- Put tests under `tests/`.
- Keep documentation in Markdown.

## Python Guidelines

- Use standard Python formatting conventions.
- Use type hints when they improve readability.
- Avoid broad `except Exception` blocks unless re-raising with useful context.
- Keep module-level constants clear and named.

## Spark Guidelines

- Create Spark sessions in a controlled location.
- Use Spark SQL for the required transformation.
- Register a temporary view before running SQL.
- Keep the SQL query readable.
- Stop Spark sessions where appropriate in tests or scripts.

## Error Handling

- Validate that input files exist before processing.
- Validate that required columns are present.
- Raise clear errors for invalid inputs.
- Do not silently continue after failed reads, writes, or validations.

## Logging

- Use simple logging or clear console output.
- Do not add external logging dependencies.
- Log major pipeline steps if helpful for learning.

## Comments

- Add comments only when they clarify non-obvious behavior.
- Do not comment every line.
- Prefer readable names over explanatory comments.

## Documentation In Code

- Public functions should have concise docstrings when useful.
- Keep examples in `README.md`, not scattered through implementation files.

## Notes For AI Agents

- Match the existing project style.
- Keep edits scoped to the requested change.
- Do not add new dependencies unless required by the OpenSpec change.
