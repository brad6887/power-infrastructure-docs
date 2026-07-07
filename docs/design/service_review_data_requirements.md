# Service Review Data Requirements

## Purpose

This document defines the data required for the Power Infrastructure monthly Service Review workflow.

The initial scope is intentionally limited to the infrastructure data currently maintained by the Power Infrastructure owner. Once this workflow is reliable, it can be expanded to include additional service review sections owned by other teams.

## Objectives

The Service Review workflow should:

- Eliminate manual monthly data collection wherever practical.
- Generate repeatable executive reports.
- Preserve engineering-level detail separately from executive summaries.
- Produce consistent deliverables every month.

## Executive Service Review Scope

The initial Service Review consists of three deliverables.

### 1. IBM Power CPU Capacity

Purpose:

Demonstrate monthly CPU utilization compared to allocated processor capacity.

Current Status:

Implemented.

Current Inputs:

- HMC Performance Export

Current Outputs:

- CPU utilization chart
- Executive summary

Future Enhancements:

- Automatic HMC collection
- Capacity observations
- Historical trend analysis

---

### 2. Pure Storage Capacity

Purpose:

Show overall storage utilization for each production array.

Required Values:

| Array | Required Metric |
|--------|-----------------|
| TXPUREP01 | Percent Used |
| COPURE01 | Percent Used |

Current Source:

Pure1 Dashboard

Preferred Future Source:

Pure REST API

Fallback Source:

Pure CLI

Executive Output:

Only the percentage used for each array.

Engineering Output:

Additional metrics such as:

- Total Capacity
- Used Capacity
- Data Reduction
- IOPS
- Bandwidth
- Latency

---

### 3. Pure ActiveDR Replication

Purpose:

Verify DR replication health.

Required Values:

- Source Pod
- Target Pod
- Replication Status
- Current Lag

Current Source:

Pure1 Dashboard

Preferred Future Source:

Pure REST API

Fallback Source:

Pure CLI

Executive Output:

Healthy / Unhealthy status and current lag.

Engineering Output:

Additional replication metrics and historical information.

Note:

The retention policy table currently included on the presentation slide is static documentation and is not part of the automation scope.

---

## Executive vs Engineering Profiles

### Executive Profile

Audience:

Monthly Service Review meeting.

Contents:

- CPU Capacity chart
- Pure Capacity summary
- ActiveDR summary
- Brief observations

The objective is to communicate overall service health, not engineering detail.

### Engineering Profile

Audience:

Infrastructure Engineering

Contents:

- Source metadata
- Validation results
- Import logs
- Capacity calculations
- Normalized datasets
- Historical metrics
- Report generation details

The engineering profile serves as supporting documentation and troubleshooting material.

---

## Future Collection Strategy

### HMC

Current:

Manual performance export.

Future:

Automatic collection using HMC CLI or API.

### Pure Storage

Current:

Manual retrieval from Pure1.

Future:

Automatic collection using the Pure REST API.

Pure CLI may be used as an intermediate implementation while learning the API.

---

## Initial Deliverables

The first automated Service Review package should produce:

```text
reports/
└── service-review/
    └── YYYYMM/
        ├── executive_summary.md
        ├── cpu_capacity.md
        ├── pure_capacity.md
        ├── replication.md
        └── charts/
            └── cpu_usage_vs_allocated.png
```

Future deliverables may include:

- PowerPoint
- PDF
- Website
- Email package
- ZIP archive

---

## Long-Term Goal

The desired monthly workflow is:

```bash
pwr playbook service-review --period YYYYMM
```

The playbook will:

1. Prepare the environment.
2. Collect HMC data.
3. Collect Pure Storage data.
4. Import source data.
5. Validate imported data.
6. Normalize vendor-specific data.
7. Generate Service Review widgets.
8. Assemble the Service Review deliverable.
9. Publish or archive the deliverable.
10. Update generated documentation automatically.
