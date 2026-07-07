# Service Review Framework

## Purpose

The Service Review Framework defines the repeatable process for collecting, validating, reporting, and packaging monthly infrastructure service review data.

The framework exists to replace manually assembled monthly review artifacts with a validated, repeatable workflow.

## Scope

The initial scope includes:

- HMC performance data
- HMC inventory data
- Pure Storage capacity and replication data
- Generated service review reports
- Generated service review deliverables

## Workflow

Service review workflows follow this sequence:

    Request
        ↓
    Prepare
        ↓
    Collect
        ↓
    Import
        ↓
    Validate
        ↓
    Normalize
        ↓
    Report
        ↓
    Deliverable
        ↓
    Publish

## Principles

- Source data is preserved unchanged.
- Normalized data is generated from source data.
- Reports are generated from normalized data.
- Service review deliverables are generated from reports.
- Documentation and indexes are generated automatically.
- Manual collection is allowed during early phases but must be replaceable by automated collection.

## Data Sources

### HMC

Used for:

- Managed system performance
- CPU capacity reporting
- Managed system inventory
- LPAR inventory

### Pure Storage

Used for:

- Array capacity
- Volume utilization
- Pod status
- Replication status
- Storage growth reporting

## Initial Service Review Scope

The initial Service Review Playbook only covers the infrastructure data currently owned by the Power Infrastructure maintainer.

### Required Monthly Outputs

| Area | Output | Source | Status |
|---|---|---|---|
| IBM Power | CPU usage vs allocated chart | HMC performance export | Working |
| Pure Storage | Array used capacity percent | Pure1 / Pure CLI / API | Planned |
| Pure Storage | ActiveDR health and lag | Pure1 / Pure CLI / API | Planned |

### Out of Scope For Initial Version

- Other teams' service review sections
- Full environment reporting
- Detailed engineering reports
- Automated PowerPoint generation
- Email delivery

These may be added after the initial owner-specific service review workflow is reliable.

## Deliverables

The framework supports multiple deliverable profiles.

### Service Review Profile

Presentation-friendly output with minimal technical detail.

### Full Profile

Detailed engineering output including:

- Collection metadata
- Validation results
- Capacity observations
- Historical metrics
- Source traceability

## Long-Term Goal

Long-term execution should be as simple as:

```bash
pwr playbook service-review --period YYYYMM
```

The playbook should:

1. Collect required data.
2. Validate collected data.
3. Import source artifacts.
4. Normalize vendor-specific data.
5. Generate reports.
6. Build the monthly service review deliverable.
7. Publish the deliverable if requested.
8. Update generated documentation automatically.
