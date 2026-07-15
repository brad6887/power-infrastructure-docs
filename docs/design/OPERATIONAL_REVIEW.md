# Operational Review Framework

## Purpose

The Operational Review Framework provides a standard, read-only process for collecting operational data, validating system health, analyzing findings, and generating consistent reports.

Operational Reviews help engineers understand the current state of an environment before planning or executing changes.

Operational Reviews must not modify managed systems.

---

## Goals

The framework should:

- provide repeatable operational assessments
- standardize health checks across infrastructure domains
- separate data collection from analysis
- produce consistent PASS, WARN, FAIL, and INFO findings
- generate operational documentation
- identify risks before maintenance or change activity
- reuse inventory and validation components
- provide a foundation for future automation workflows

---

## Core Principle

An Operational Review answers:

> What is the current state of the environment?

The Workflow Engine answers:

> How can the environment be changed safely?

Operational Reviews observe and document state.

Workflows validate, plan, execute, and verify changes.

---

## Review Lifecycle

Every Operational Review follows the same lifecycle.

```text
Initialize
    |
    v
Collect
    |
    v
Validate
    |
    v
Analyze
    |
    v
Summarize
    |
    v
Report
```

### Initialize

Prepare the review execution.

Responsibilities include:

- parsing command-line arguments
- resolving target systems
- loading configuration
- validating inventory membership
- recording review metadata

### Collect

Gather raw operational information from authoritative sources.

Collection should avoid interpreting results whenever practical.

Examples include:

- AIX commands
- HMC commands
- VIOS commands
- IBM MQ commands
- Pure Storage CLI/API
- Veeam APIs
- Generated inventory

### Validate

Evaluate collected data against expected operational requirements.

Examples:

- required services are running
- queue managers are active
- replication is current
- filesystem usage is below threshold
- required adapters exist

### Analyze

Transform collected information into engineering findings.

Analysis identifies:

- healthy conditions
- warnings
- failures
- operational risks
- unusual conditions

### Summarize

Produce a concise engineering assessment.

The summary includes:

- overall status
- PASS count
- WARN count
- FAIL count
- key observations
- recommended actions

### Report

Generate documentation.

Initial formats:

- Console
- Markdown

Future formats:

- JSON
- HTML
- Dashboards
- Historical reports

---

## Status Model

Every finding uses one of four statuses.

### PASS

Requirement satisfied.

Example:

```text
PASS  Queue Manager TXWCSP11 is running.
```

### WARN

Condition requires attention.

Example:

```text
WARN  Queue EUMFSEDC depth exceeds threshold.
```

### FAIL

Requirement not satisfied.

Example:

```text
FAIL  MQ Listener is not running.
```

### INFO

Useful information that is not evaluated.

Example:

```text
INFO  Queue Manager uptime is 17 days.
```

---

## Overall Review Status

Overall review status follows this precedence.

```text
FAIL
WARN
PASS
```

Rules:

- Any FAIL → FAIL
- Else if WARN exists → WARN
- Else → PASS

INFO findings do not affect overall status.

UNKNOWN may be used when sufficient data cannot be collected.

---

## Standard Finding Structure

```yaml
status: PASS
check: mq_queue_manager_running
summary: Queue Manager TXWCSP11 is running
details: Queue manager returned RUNNING
source: dspmq
target: txwcsp11
recommendation: null
```

---

## Standard Review Structure

```yaml
review:

  name: mq
  target: txwcsp11
  status: PASS

  summary:
    pass: 8
    warn: 0
    fail: 0
    info: 3

  findings:

    - status: PASS
      summary: Queue Manager is running

  recommendations: []

  generated_files:
    - docs/generated/reviews/mq/txwcsp11.md
```

Every review should emit the same logical structure regardless of technology.

---

## Command Line Interface

```text
pwr review

pwr review list

pwr review mq

pwr review aix

pwr review filesystem

pwr review hmc

pwr review vios

pwr review pure

pwr review backup
```

Review implementations remain hidden behind the CLI.

The operator should not need to know whether the implementation uses Ansible, shell scripts, Python, or APIs.

---

## Proposed Repository Layout

```text
reviews/

    mq/

        collect.yml

        validate.yml

        analyze.yml

        report.yml

    filesystem/

    aix/

    pure/

roles/

    operational_review/

        initialize/

        summarize/

        report/
```

This structure should only be adopted after the framework has been validated through real implementations.

---

## Reference Implementation

The existing MQ Health playbook becomes the first Operational Review.

Current:

```bash
pwr playbook mq-health
```

Future:

```bash
pwr review mq
```

The first implementation should introduce:

- common status model
- common findings
- common summary
- Markdown reporting

while preserving existing operational behavior.

---

## Safety Requirements

Operational Reviews:

- never modify managed systems
- never restart services
- never change configuration
- never perform remediation
- preserve collected evidence
- report incomplete data rather than guessing

Any corrective action belongs in the Workflow Engine.

---

## Relationship to Inventory

Operational Reviews consume the generated inventory.

Reviews may report inventory inconsistencies.

They do not silently correct inventory.

---

## Relationship to Documentation

Operational Reviews generate documentation.

Reports should contain:

- target
- timestamp
- overall status
- findings
- recommendations
- collected evidence
- project version

Generated reports become operational records suitable for:

- change preparation
- incident review
- audit evidence
- lifecycle planning

---

## Initial Implementation Plan

1. Design Operational Review Framework.
2. Add `pwr review`.
3. Add `pwr review list`.
4. Route `pwr review mq` to the existing MQ implementation.
5. Introduce standard findings.
6. Introduce standard summaries.
7. Generate Markdown reports.
8. Preserve compatibility with `mq-health`.
9. Validate framework with a second review.
10. Refine architecture based on experience.

---

## Candidate Reviews

- MQ
- AIX
- Filesystem
- Services
- HMC
- VIOS
- Pure Storage
- Backup
- Disaster Recovery

MQ serves as the reference implementation.

Filesystem is likely the second implementation because it is simple and broadly useful.

---

## Design Decisions

- Reviews are read-only.
- Reviews are separate from automation workflows.
- Reviews generate documentation.
- Reviews use a common status model.
- Reviews produce a common result structure.
- Existing production logic should be reused whenever practical.
- Framework design evolves from working implementations.

---

## Future Enhancements

Possible future capabilities include:

- HTML reports
- JSON output
- Historical comparisons
- Trend analysis
- Health scoring
- Dashboard integration
- Scheduled reviews
- Review archives
