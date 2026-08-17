# Data And Security Guardrails

## Purpose

This document defines organization or team-level data, privacy, and security
expectations. It should not contain project-specific schemas, field names, tables,
files, credentials, or business data structures.

Change-specific data and security details belong in the change context, such as:

- `changes/<change-name>/INTENT.md`
- `changes/<change-name>/ACCEPTANCE_CRITERIA.md`
- `changes/<change-name>/OUT_OF_SCOPE.md`
- A dedicated `changes/<change-name>/DATA_CONTRACT.md` when the contract is large
- A dedicated `changes/<change-name>/SECURITY_NOTES.md` when security decisions are substantial

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
- Row-level filtering, aggregation, or deduplication behavior.
- Ownership of the data contract.

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

## Privacy Rules

- Do not use real personal data in demos, tests, or examples.
- Sensitive fields must be identified in the change-specific data contract.
- Sensitive fields must not be logged, written to unsafe outputs, or included accidentally.
- Masking, dropping, hashing, or tokenization decisions must be documented.

## Secrets Rules

- Do not commit credentials, tokens, API keys, passwords, certificates, or private keys.
- Changes requiring secrets must document the approved secret source.
- Local examples should avoid secrets unless they are essential to the learning goal.

## External Service Rules

- Do not introduce external services unless they are explicitly in scope.
- Do not add cloud storage, databases, APIs, or queues without documenting why.
- New external integrations must describe data sent, data received, authentication, and failure behavior.

## Local Filesystem Safety

- Source data must not be overwritten unless explicitly approved.
- Output locations must be documented.
- Destructive behavior must be explicit and avoided by default.

## Dependency Safety

- Keep dependencies minimal.
- Do not add new dependencies without a clear need.
- Prefer established packages already approved in the tech platform.

## Logging Safety

- Do not log sensitive fields.
- Do not print full source records when they may contain sensitive, internal, or regulated data.
- Error messages should help debugging without exposing protected values.

## Notes For AI Agents

- Do not invent data contracts.
- Read the change-specific context for actual source and output structures.
- Ask clarification questions when source fields, output fields, sensitive fields, or security expectations are unclear.
- Treat data and security requirements as required behavior, not implementation detail.
- If a requested change weakens these guardrails, ask for clarification before proceeding.
