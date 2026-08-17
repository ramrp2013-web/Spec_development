# Out Of Scope: Create Customer Medallion Pipeline

This first version should not include unless explicitly selected during explore:

- Airflow or any other scheduler.
- Production deployment.
- Real customer data.
- Data catalog integration.
- Secrets management.
- Monitoring dashboards.
- CI/CD setup.
- Containerization.
- Complex business aggregations.
- Cross-domain joins.
- Machine learning features.
- Real-time serving APIs.

The following are source and target options, not automatically in scope:

- Relational database ingestion.
- Kafka ingestion.
- Cloud storage such as ADLS.
- Data warehouse writes.
- Relational Data Mart writes.

If one of these source or target options is selected during explore, it becomes
part of this change's scope. Otherwise, it requires a separate intent and
OpenSpec change.
