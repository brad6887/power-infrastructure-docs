# Operational Health Framework

## Purpose

The Operational Health Framework provides a consistent method for validating, collecting, evaluating, explaining, and reporting infrastructure health across the Power Infrastructure platform.

The framework is intended for rapid operational assessment when an engineer is asked questions such as:

- Is MQ healthy?
- Is the AIX host healthy?
- Is storage replication current?
- Is the backup environment functioning?
- Is the problem within infrastructure or downstream?

The framework does not replace product-specific administration or deep troubleshooting. Its purpose is to provide an evidence-based first assessment and guide the operator toward the next appropriate investigation.

---

## Core Principle

Operational health checks should do more than display command output.

Every health check should answer:

1. What was checked?
2. What evidence was collected?
3. Is the result healthy?
4. What does the result mean?
5. Why does it matter?
6. What should the operator investigate next?

---

## Standard Health Workflow

```text
Prepare
    ↓
Validate
    ↓
Collect
    ↓
Evaluate
    ↓
Summarize
    ↓
Explain
    ↓
Recommend
    ↓
Report
    ↓
Document
    ↓
Archive
```

Health workflows are read-only unless a separate, explicitly approved remediation workflow is invoked.

A health workflow must not automatically:

- Restart services.
- Start or stop queue managers.
- Reset channels.
- Clear queues.
- Change storage paths.
- Expand filesystems.
- Modify configuration.
- Remove files.
- Perform other corrective actions.

---

## Relationship to the Workflow Engine

Operational health workflows use the standard Power Infrastructure Workflow Engine.

The Workflow Engine provides:

- Workflow context.
- Execution timestamps.
- Operator identity.
- Workspace creation.
- Stage management.
- Artifact tracking.
- Reporting.
- Documentation.
- Archival.

Domain-specific health workflows provide:

- Validation logic.
- Collection commands.
- Evaluation rules.
- Technology-specific explanations.
- Recommendations.

Examples include:

```text
mq-health
aix-health
vios-health
hmc-health
pure-health
veeam-health
oracle-health
```

---

## Health Check Model

Each health check should produce a standard result object.

Example:

```yaml
health_checks:
  - id: mq.queue_manager
    title: Queue Manager
    technology: mq
    target: txwcsp11
    status: PASS
    summary: Queue manager TXWCSP11 is running
    meaning: MQ is available to process work.
    why_it_matters: Applications cannot use MQ when the queue manager is unavailable.
    recommendation: ""
    evidence:
      command: dspmq -m TXWCSP11
      status: STATUS(Running)
```

The common structure allows the same reporting logic to be reused for different technologies.

---

## Required Result Fields

Each health check should contain:

| Field | Purpose |
|---|---|
| `id` | Stable machine-readable identifier |
| `title` | Human-readable check name |
| `technology` | Technology or platform |
| `target` | Host, queue manager, array, frame, or other target |
| `status` | PASS, INFO, WARN, FAIL, or ERROR |
| `summary` | Concise factual result |
| `meaning` | Plain-language interpretation |
| `why_it_matters` | Operational importance |
| `recommendation` | Suggested next action when appropriate |
| `evidence` | Structured supporting facts |

Optional fields may include:

```yaml
question:
expected:
observed:
threshold:
source:
started_at:
completed_at:
duration_seconds:
```

---

## Status Definitions

### PASS

The observed result matches the healthy expectation.

Example:

```text
PASS Queue Manager
Queue manager TXWCSP11 is running.
```

### INFO

The result is informational and does not indicate a problem.

Example:

```text
INFO System Queues
Eight internal MQ queues contain messages.
```

### WARN

The result may require attention but does not prove a service outage.

Example:

```text
WARN Filesystem Capacity
/var is 86 percent utilized.
```

### FAIL

The observed result indicates a failed health condition.

Example:

```text
FAIL NTP Service
xntpd is not running.
```

### ERROR

The check could not be completed or the evidence is unreliable.

Example:

```text
ERROR Disk Path Check
The target host could not be reached.
```

A collection error must not be reported as a failed infrastructure condition.

---

## Overall Status

The overall workflow status is derived from individual checks.

Recommended precedence:

```text
ERROR
FAIL
WARN
INFO
PASS
```

Suggested behavior:

- Any `ERROR` result makes the overall status `ERROR`.
- Otherwise, any `FAIL` result makes the overall status `FAIL`.
- Otherwise, any `WARN` result makes the overall status `WARN`.
- Otherwise, the overall status is `PASS`.
- `INFO` results do not lower an otherwise healthy status.

---

## Separation of Responsibilities

### Validation

Confirms that the workflow can run safely and meaningfully.

Examples:

- Target exists in inventory.
- Host is reachable.
- Required commands exist.
- Required input is provided.
- Required permissions are available.

### Collection

Collects raw evidence without deciding whether the result is healthy.

Examples:

- `dspmq`
- `DISPLAY CHSTATUS(*)`
- `df -k`
- `lspath`
- `errpt`

### Evaluation

Applies documented rules and thresholds to collected evidence.

Examples:

- Queue manager is running.
- Channel is retrying.
- Filesystem is above 80 percent.
- Disk paths are missing.
- NTP service is stopped.

### Explanation

Describes what the result means in plain operational language.

### Recommendation

Provides the next investigative action without automatically changing the environment.

### Reporting

Presents results in a consistent operator-focused format.

---

## Evidence Requirements

Every conclusion must be traceable to collected evidence.

A report should distinguish between:

```text
Observed
Expected
Interpretation
Recommendation
```

Example:

```text
Observed
Channel TXWCSP11.NDCP is RUNNING.

Expected
Production sender channels should be RUNNING while actively processing work.

Interpretation
MQ communication with the remote queue manager appears operational.

Recommendation
No action required.
```

Health reports should avoid unsupported conclusions.

For example, a growing transmission queue may indicate downstream processing delay, but it does not by itself prove the downstream system is the cause.

---

## Thresholds and Expectations

Thresholds should be stored in configuration or inventory metadata whenever possible.

Example:

```yaml
health:
  aix:
    filesystem_warning_percent: 80
    filesystem_critical_percent: 90
    errpt_window_hours: 24
    expected_disk_paths_per_disk: 8

  mq:
    error_window_minutes: 60
    fdc_window_hours: 24
```

Target-specific exceptions should also be represented as metadata.

Example:

```yaml
txwcsp11:
  mq:
    queue_manager: TXWCSP11
    expected_listeners:
      - TCP.LISTENER
      - SYSTEM.LISTENER.TCP.1
```

Hard-coded environment assumptions should be avoided inside roles.

---

## Operator Report

A standard operator report should include:

```text
Health Check
Target
Timestamp
Overall Status
Summary
Checks
Evidence
Meaning
Recommendations
Artifact Location
```

Example:

```text
MQ Health
=========

Host............... txwcsp11
Queue Manager...... TXWCSP11
Overall Status..... PASS

PASS Queue Manager
  TXWCSP11 is running.

  Meaning:
  MQ is available to process work.

PASS Listeners
  Two listeners are running.

  Meaning:
  Remote applications can establish MQ connections.

PASS Channels
  Two channels are running.
  No retrying channels were found.

INFO System Queues
  Eight internal queues contain messages.

  Meaning:
  Internal MQ queues commonly contain operational state.
```

---

## Structured Artifacts

Each workflow should eventually generate:

```text
summary.txt
report.md
results.json
evidence/
```

Example:

```text
docs/generated/ad-hoc/mq-health-20260713-083121/
├── summary.txt
├── report.md
├── results.json
└── evidence/
    ├── dspmq.txt
    ├── qmstatus.txt
    ├── listener_status.txt
    ├── channel_status.txt
    ├── queue_status.txt
    ├── amqerr01.log
    └── fdc_files.txt
```

The structured JSON result is the authoritative machine-readable output.

Markdown and text reports are generated from the structured result.

---

## AI Integration

AI is optional and must not be required for workflow execution.

The authoritative health result must be produced using deterministic collection and evaluation logic.

An approved AI service may later consume sanitized structured artifacts to:

- Summarize results.
- Draft bridge-call updates.
- Produce ticket comments.
- Generate change documentation.
- Explain unfamiliar terminology.
- Suggest investigative questions.

AI should not:

- Replace evidence collection.
- Determine production state without deterministic checks.
- Execute corrective actions.
- Receive credentials or restricted data.
- Become a required dependency for health workflows.

The framework should remain fully useful without AI integration.

---

## Initial Reference Implementations

The first reference implementations are:

### MQ Health

Checks:

- Queue manager state.
- Listener state.
- Channel state.
- Queue depth.
- MQ error log.
- Recent FDC files.

### AIX Health

Initial checks:

- NTP service.
- Bootlist.
- Disk paths.
- Filesystem utilization.

Future AIX checks may include:

- Mksysb coverage.
- Paging-space utilization.
- Error report analysis.
- Volume-group state.
- Dump-device readiness.
- CPU and memory utilization.
- OS maintenance level.
- Cron failures.
- Remote-restart readiness.
- Preferred frame placement.

---

## Long-Term Direction

The Operational Health Framework should become the standard first-response assessment mechanism for infrastructure incidents.

The operator experience should remain consistent regardless of technology:

```bash
pwr health mq --host txwcsp11
pwr health aix --host txwcsp11
pwr health pure --array TXPUREP01
pwr health veeam
```

Each command should provide:

- Objective evidence.
- Consistent status classifications.
- Plain-language explanations.
- Recommended next steps.
- Generated documentation.
- Historical artifacts.
