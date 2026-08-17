# Security Guardrails

## Purpose

This document defines security and privacy guardrails for the CSV Spark SQL
pipeline example.

## Data Privacy

- Do not use real customer data.
- Use synthetic sample records only.
- Treat the dropped fields in `DATA_GUARDRAILS.md` as sensitive or internal fields.
- Exclude sensitive or internal fields from the transformed output.

## Secrets

- No secrets are required for this local example.
- Do not add credentials, tokens, API keys, or passwords.
- Do not commit secrets to files.

## External Services

- Do not call external services.
- Do not add cloud storage.
- Do not add databases.
- Do not add third-party APIs.

## Local Filesystem Safety

- Do not overwrite source data.
- Write output only to documented output locations.
- Make destructive behavior explicit and avoid it by default.

## Dependency Safety

- Keep dependencies minimal.
- Do not add new dependencies without a clear need.
- Prefer established packages already approved in the tech platform.

## Logging Safety

- Do not log sensitive or internal dropped fields.
- Do not print full source records if they contain fields that should be dropped.

## Notes For AI Agents

- If a requested change weakens these guardrails, ask for clarification before proceeding.
- Security and privacy guardrails override convenience.
