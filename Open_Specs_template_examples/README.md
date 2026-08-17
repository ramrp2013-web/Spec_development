# OpenSpec Template Examples

This folder shows one way to standardize OpenSpec context across teams.

Use `standards/` for reusable team guidance and `changes/<change-name>/` for
change-specific context.

## Standards Files

| File | Purpose |
|---|---|
| `standards/TECH_PLATFORM.md` | Defines approved languages, runtimes, Spark/Spark SQL platform expectations, source/target options, dependency rules, and version constraints. |
| `standards/ARCHITECTURE_DESIGN_GUIDELINES.md` | Defines architecture and design expectations, including boundaries, component design, contracts, error handling, observability, resilience, and documentation. |
| `standards/CODING_GUIDELINES.md` | Defines coding style, project organization, data access rules, transformation rules, error handling, logging, and agent coding expectations. |
| `standards/TESTING_GUIDELINES.md` | Defines testing expectations for unit, integration, contract, data, and edge-case tests. |
| `standards/DATA_SECURITY_GUARDRAILS.md` | Defines data handling, privacy, secrets, external service, filesystem, dependency, and logging guardrails. |

## Change-Specific Files

Example change:

```text
changes/create-customer-pipeline/
```

| File | Purpose |
|---|---|
| `INTENT.md` | Explains the goal, problem, audience, medallion flow, layer expectations, source/target options, and explore questions. |
| `CURRENT_STATE.md` | Describes existing source systems, databases, topics, files, tables, pipelines, consumers, pain points, and constraints. |
| `SOURCE_CONTRACT.md` | Defines the source type, location, owner, schema, read mode, incremental logic, data quality rules, and rejected-record strategy. |
| `PIPELINE_DESIGN.md` | Describes the intended Source -> Landing / Raw -> Bronze -> Silver -> Gold -> Data Mart flow, layer purpose, storage, rules, proposed code structure, data quality strategy, and rejected-record strategy. |
| `ACCEPTANCE_CRITERIA.md` | Defines functional, data, testing, documentation, and OpenSpec completion criteria. |
| `OUT_OF_SCOPE.md` | Lists items that should not be built unless explicitly selected during explore. |

## Suggested Read Order For Explore

```text
1. standards/TECH_PLATFORM.md
2. standards/ARCHITECTURE_DESIGN_GUIDELINES.md
3. standards/CODING_GUIDELINES.md
4. standards/TESTING_GUIDELINES.md
5. standards/DATA_SECURITY_GUARDRAILS.md
6. changes/create-customer-pipeline/INTENT.md
7. changes/create-customer-pipeline/CURRENT_STATE.md
8. changes/create-customer-pipeline/SOURCE_CONTRACT.md
9. changes/create-customer-pipeline/PIPELINE_DESIGN.md
10. changes/create-customer-pipeline/ACCEPTANCE_CRITERIA.md
11. changes/create-customer-pipeline/OUT_OF_SCOPE.md
```

## Example Explore Prompt

```text
$openspec-explore

Read the standards files and the create-customer-pipeline change files.

Explore this medallion pipeline before creating an OpenSpec proposal. Ask
clarification questions about source type, read mode, Landing / Raw, Bronze,
Silver, Gold, Data Mart targets, Spark SQL transformations, data contracts,
data quality rules, rejected records, code/folder structure, security guardrails,
and test strategy.
```

## Example Propose Prompt

Use this after explore questions are answered and the change is ready to become
formal OpenSpec artifacts.

```text
$openspec-propose create-customer-medallion-pipeline

Read the standards files and the create-customer-pipeline change files.

Create an OpenSpec change for the customer medallion pipeline.

The proposal should cover:

- Source -> Landing / Raw -> Bronze -> Silver -> Gold -> Data Mart.
- Spark and Spark SQL as required processing technologies.
- The selected source type and read mode.
- The selected target type and write mode.
- Layer contracts for Landing / Raw, Bronze, Silver, Gold, and Data Mart.
- Proposed code/folder structure from PIPELINE_DESIGN.md.
- Data quality and rejected-record behavior.
- Security and sensitive-field handling.
- Testing and validation expectations.

Generate proposal, spec, design, and tasks before implementation.
```

## Example Update Change Prompt

Use this when the generated OpenSpec change needs revision before or during
implementation.

```text
$openspec-update-change create-customer-medallion-pipeline

Update the OpenSpec change based on the following clarification:

<fill in clarification>

Re-check the standards and change-specific context. Update the proposal, spec,
design, and tasks as needed so they remain aligned with the medallion architecture,
Spark SQL transformation requirement, data contracts, acceptance criteria, and
out-of-scope boundaries.
```

## Example Apply Change Prompt

Use this after the OpenSpec proposal, spec, design, and tasks have been reviewed
and approved.

```text
$openspec-apply-change create-customer-medallion-pipeline

Implement the approved customer medallion pipeline change.

Read the generated OpenSpec files first:

- proposal.md
- design.md
- tasks.md
- specs/<capability>/spec.md

Then implement the tasks step by step.

While implementing:

- Follow the standards files.
- Use Spark and Spark SQL for transformation work.
- Preserve the approved medallion layer behavior.
- Keep source and target behavior aligned with the selected design.
- Add or update tests for each required behavior.
- Update task checkboxes only after the work is complete and verified.
```

## Example Sync Specs Prompt

Use this if files were edited manually or the implementation and specs may have
drifted.

```text
$openspec-sync-specs

Review the current implementation, standards files, active OpenSpec change, and
permanent specs.

Report whether the customer medallion pipeline specs are still aligned with the
current project state. If anything is out of sync, explain what needs to change
before implementation continues or before archive.
```

## Example Archive Prompt

Use this after implementation is complete, tests pass, and the change is ready to
become permanent project behavior.

```text
$openspec-archive-change create-customer-medallion-pipeline

Archive the completed customer medallion pipeline change.

Before archiving, confirm:

- All tasks are complete.
- Required tests pass.
- OpenSpec validation passes.
- The implementation follows the approved medallion design.
- Permanent specs will reflect the final behavior.
```
