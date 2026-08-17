# Tech Platform

## Purpose

This document defines the approved technical platform for a team or project.
OpenSpec and AI coding agents should use it when exploring, proposing, designing,
and implementing changes.

It should describe the allowed technology landscape without embedding
change-specific schemas, business rules, or one-off implementation details.

## Project Type

Data engineering pipeline or batch data transformation job.

## Primary Languages

- Python.
- SQL.

## Runtime Environment

Approved runtime options:

- Local developer machine.
- Docker.
- Managed Spark platform.
- Databricks job.
- Batch compute cluster.

Each change must identify the selected runtime.

## Frameworks And Libraries

Required processing platform:

- Apache Spark.
- PySpark.
- Spark SQL.

Approved supporting libraries:

- pytest for Python tests.
- Approved database drivers or connectors when the selected source or target is relational.
- Approved cloud storage connectors when the selected source or target is cloud storage.

## Package Management

Define dependency management expectations.

Examples:

- `requirements.txt`.
- Poetry.
- uv.
- pnpm.
- npm.
- Maven.
- Gradle.

## Source And Data Platform

Document the approved source and target platforms for the team.

Allowed source types may include:

- Local or cloud files.
- Relational database tables.
- Data warehouse tables.

Allowed target types may include:

- Local files.
- Cloud files, including ADLS when approved for the change.
- Relational database tables.
- Data warehouse tables.

Each change must specify its actual source and target in the change-specific context.

## Infrastructure Platform

List approved infrastructure choices.

Examples:

- Local-only.
- Docker Compose.
- AWS.
- Azure.
- GCP.
- Kubernetes.
- Terraform-managed infrastructure.
- Managed orchestration platform.

## Testing Platform

Define approved testing tools and expectations.

- pytest.
- Spark local mode for local tests when feasible.
- Contract tests for source and target schemas.
- Local database or containerized database for relational tests when approved.
- Sample files or synthetic data fixtures.

## CI/CD Platform

State the approved build, test, and deployment platform.

Examples:

- GitHub Actions.
- GitLab CI.
- Jenkins.
- Azure DevOps.
- Manual local validation for learning examples.

## Observability Platform

Define logging, metrics, tracing, and alerting expectations.

Examples:

- Console logs.
- Structured application logs.
- OpenTelemetry.
- CloudWatch.
- Datadog.
- Splunk.

## Security And Secrets

Define approved secrets handling.

Examples:

- Environment variables for local development.
- Cloud secrets manager.
- Vault.
- Managed identity.
- Service account.

Secrets must not be committed to source control.

## Version Constraints

Use this table to define version expectations.

| Tool | Required Version | Notes |
|---|---:|---|
| Python | `<fill in>` | Required for PySpark implementation |
| Java | `<fill in>` | Required by Spark runtime when applicable |
| Spark | `<fill in>` | Required processing engine |
| PySpark | `<fill in>` | Required Python Spark API |
| pytest | `<fill in>` | Required test framework |

## Approved Technologies

- Python
- SQL
- Apache Spark
- PySpark
- Spark SQL
- pytest
- Local files
- Approved relational connectors
- Approved cloud storage connectors

## Restricted Technologies

List technologies that require explicit approval before use.

Examples:

- New database engines or warehouse platforms.
- New cloud services.
- New orchestration platforms.
- New external APIs.
- New paid services.
- Experimental frameworks.

## Default Local Development Setup

Provide generic local setup guidance or point to the project README.

```bash
<fill in project-specific setup commands>
```

## Notes For AI Agents

- Use only the approved platform choices.
- Spark and Spark SQL are required for transformation work in this template.
- Do not introduce new runtime, storage, database, cloud, or framework dependencies without approval.
- Source may be file-based or relational; ask for clarification before proposing implementation.
- Target may be local, cloud storage such as ADLS, or relational; ask for clarification before proposing implementation.
- Read the change-specific context for the actual source, target, and data contract.
