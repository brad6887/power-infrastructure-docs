# Data Pipeline Standards

## Purpose

This document defines the standard pattern for collecting, preserving, normalizing, and reporting infrastructure data in Power Infrastructure.

## Pipeline Model

All data-driven workflows should follow this pattern:

```text
Acquire
    ↓
Import
    ↓
Validate
    ↓
Normalize
    ↓
Generate
    ↓
Document
```

## Data Directories

### Source Data

Source data is vendor output preserved as close to original as possible.

```text
inventory/source/<technology>/<collection-date>/
```

Examples:

```text
inventory/source/pure/2026-07-07/
inventory/source/hmc/performance/2026-07-07/
```

Source data should not be manually edited.

### Normalized Data

Normalized data is generated from source data and used by reports.

```text
inventory/normalized/<technology>/
```

Examples:

```text
inventory/normalized/pure/202607_capacity.csv
inventory/normalized/hmc/performance/202606_cpu_daily.csv
```

### Generated Reports

Reports are generated from normalized data.

```text
reports/<report-category>/<period>/
```

Examples:

```text
reports/capacity/202606/
reports/storage/202607/
```

## Collection Dates and Reporting Periods

Collection dates use:

```text
YYYY-MM-DD
```

Reporting periods use:

```text
YYYYMM
```

Collection date and reporting period are different concepts.

Example:

```text
Collection date: 2026-08-01
Reporting period: 202607
```

## Manifest Files

Each source collection should include a manifest.

```text
manifest.yml
```

The manifest records:

- collector
- collection date
- status
- systems or arrays collected
- source files created

Example:

```yaml
collector: pure-cli
collection_date: 2026-07-07
status: collected

arrays:
  - txpurep01
  - copure01

files:
  - txpurep01_array_space.csv
  - txpurep01_connections.csv
  - txpurep01_pods.csv
  - copure01_array_space.csv
  - copure01_connections.csv
  - copure01_pods.csv
```

## Collector Rules

Collectors should:

- Acquire raw data only.
- Write source files under `inventory/source`.
- Generate a manifest.
- Avoid report logic.
- Avoid normalization logic.
- Be safe to rerun when practical.

## Normalizer Rules

Normalizers should:

- Read source data.
- Produce standard datasets.
- Write to `inventory/normalized`.
- Avoid chart or report generation.
- Hide vendor-specific formats from report generators.

## Report Generator Rules

Report generators should:

- Read normalized data.
- Write reports under `reports`.
- Avoid direct access to vendor source files.
- Update generated documentation when appropriate.

## Operational Requirement

Collectors that use SSH require passwordless SSH from the automation host.

For Pure Storage arrays, install the automation user's SSH public key with:

```text
pureadmin setattr --publickey <user>
```

Verify access before running collection commands.

## Current Implementations

### HMC Performance

Implemented:

- Source ZIP preservation
- JSON extraction
- Manifest generation
- Normalized CPU daily dataset
- CPU capacity report
- Report index update

### Pure Storage

Implemented:

- Pure CLI collection
- Manifest generation
- Capacity normalization
- Replication health normalization
- Pure capacity widget
- Report index update
