# Tech Platform

## Purpose

This document defines the approved technical platform for the CSV Spark SQL
pipeline example. OpenSpec and AI coding agents should use this file when
exploring, proposing, designing, and implementing changes for this project.

## Project Type

Data engineering batch pipeline.

## Primary Languages

- Python
- SQL

## Runtime Environment

- Local developer machine for the first version.
- Apache Spark local mode.
- No production runtime is required for this example.

## Frameworks And Libraries

- PySpark for data processing.
- Spark SQL for transformation logic.
- pytest for automated tests.

## Package Management

- Use `requirements.txt` for Python dependencies.
- Do not add a heavier packaging tool unless the change explicitly asks for it.

## Data Platform

- Input format: local CSV file.
- Output format: local CSV file.
- Processing engine: Apache Spark through PySpark.
- Query engine: Spark SQL.

## Infrastructure Platform

- Local filesystem only.
- No cloud infrastructure.
- No database.
- No scheduler.

## Testing Platform

- pytest.
- Small synthetic CSV test data.
- Local Spark session for transformation tests.

## CI/CD Platform

No CI/CD platform is required for this learning example.

## Observability Platform

- Console logs or simple Python logging are acceptable.
- No external monitoring system is required.

## Security And Secrets

- No secrets are required.
- Do not commit credentials.
- Do not use real customer data.

## Version Constraints

| Tool | Required Version | Notes |
|---|---:|---|
| Python | 3.8+ | Required by PySpark compatibility in this example |
| Java | 8+ | Required for Spark |
| PySpark | Project dependency | Define exact version in `requirements.txt` |
| pytest | Project dependency | Define exact version in `requirements.txt` |

## Approved Technologies

- Python
- PySpark
- Spark SQL
- pytest
- Local CSV files
- Markdown documentation

## Restricted Technologies

- Do not add Airflow.
- Do not add cloud storage such as S3, ADLS, or GCS.
- Do not add databases.
- Do not add streaming frameworks.
- Do not add orchestration tools.
- Do not add secrets managers.

## Default Local Development Setup

```bash
cd demos/csv-spark-sql-transform
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
pytest
python src/pipeline.py
```

## Notes For AI Agents

- Use the approved local PySpark platform.
- Do not introduce new infrastructure.
- Use Spark SQL for the transformation.
- If a requested change conflicts with this platform, ask a clarification question
  before proposing implementation.
