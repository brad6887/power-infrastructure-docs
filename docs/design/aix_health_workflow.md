# AIX Health Workflow Design

## Purpose

The AIX Health workflow provides a read-only operational assessment of AIX LPAR health.

The workflow is based on proven checks from the existing `health_check.ksh` production script while adapting the logic to the Power Infrastructure Workflow Engine and Operational Health Framework.

The existing script remains a reference implementation until the replacement workflow has been validated.

---

## Goals

The AIX Health workflow should:

- Use the authoritative Power Infrastructure inventory.
- Validate targets before collecting data.
- Separate collection from evaluation.
- Produce structured health results.
- Explain what each result means.
- Recommend the next investigative action.
- Generate operator-readable reports.
- Preserve raw evidence.
- Support multiple LPARs.
- Distinguish infrastructure failures from collection failures.
- Remain read-only.

---

## Existing Reference Implementation

The existing `health_check.ksh` script performs the following checks:

- Missing mksysb backups.
- NTP process status.
- Bootlist correctness.
- Disk path health.
- Remote restart status.
- Preferred hardware placement.
- Processor and SMT settings.
- Active System Optimizer status.
- Dump-device capacity.
- Paging-space configuration.
- Filesystem utilization.
- AIX error report.
- CPU and memory activity.
- OS maintenance level.
- Cron failures.
- Volume-group state.

This logic contains valuable operational knowledge and should be preserved where appropriate.

The new workflow should not directly copy assumptions that are tied to the old environment.

---

## Initial Scope

The first AIX Health implementation will contain four checks:

```text
NTP Service
Bootlist
Disk Paths
Filesystem Utilization
```

These checks provide high operational value and are suitable for proving the shared health-check model.

Additional checks will be added incrementally after the initial workflow is validated.

---

## Workflow

```text
Prepare
    ↓
Validate Target
    ↓
Collect AIX Evidence
    ↓
Evaluate Checks
    ↓
Build Health Results
    ↓
Generate Quick View
    ↓
Generate Report
    ↓
Store Evidence
    ↓
Archive
```

---

## Initial Checks

## NTP Service

### Question

Is the AIX time synchronization service running?

### Collection

Preferred command:

```sh
lssrc -s xntpd
```

Fallback:

```sh
ps -ef | grep '[x]ntpd'
```

### Healthy Result

```text
xntpd active
```

### Failure Result

```text
xntpd inactive or missing
```

### Why It Matters

Incorrect system time can affect:

- Authentication.
- Certificates.
- Application logs.
- Database transactions.
- Cluster operations.
- Incident timelines.
- Backup operations.

### Recommended Next Steps

- Review `lssrc -s xntpd`.
- Verify `/etc/ntp.conf`.
- Test configured NTP servers.
- Review recent AIX errors.
- Do not automatically restart the service from the health workflow.

---

## Bootlist

### Question

Does the normal bootlist reference the active `rootvg` disk or disks?

### Collection

```sh
bootlist -m normal -o
lspv
```

### Evaluation

The configured boot disk should match a disk assigned to the active `rootvg`.

Multi-disk root volume groups must be supported.

The original script used:

```sh
bootlist -m normal -o | awk '{print $1}'
lspv | grep rootvg
```

The replacement should collect and compare complete disk lists rather than assume a single boot disk.

### Why It Matters

An incorrect bootlist may prevent the LPAR from booting from the intended root volume group after a restart.

### Recommended Next Steps

- Confirm the intended rootvg disk.
- Review alternate-disk or upgrade activity.
- Review the normal bootlist.
- Correct the bootlist only through a separate approved remediation workflow.

---

## Disk Paths

### Question

Are expected MPIO disk paths available and enabled?

### Collection

```sh
lspath
lsdev -Cc disk
```

Possible supporting commands:

```sh
lspv
lsmpio
```

### Evaluation

The workflow should detect:

- Failed paths.
- Missing paths.
- Disabled paths.
- Unexpected path-count differences.

Expected path counts must come from inventory or configuration.

Example:

```yaml
expected_disk_paths_per_disk: 8
```

The workflow must not assume that every environment always has eight paths.

### Why It Matters

Missing paths reduce storage redundancy and can increase outage risk during SAN, adapter, VIOS, or switch failures.

### Recommended Next Steps

- Identify affected disks.
- Identify failed adapters or VIOS paths.
- Review SAN zoning and mappings.
- Compare path state through both VIOS servers.
- Review recent storage and adapter errors.
- Do not run `cfgmgr`, remove paths, or change storage configuration automatically.

---

## Filesystem Utilization

### Question

Are filesystems below configured capacity thresholds?

### Collection

Preferred command:

```sh
df -k
```

The implementation should parse filesystem name, mount point, total capacity, used capacity, available capacity, and utilization percentage.

### Default Thresholds

```yaml
filesystem_warning_percent: 80
filesystem_critical_percent: 90
```

Thresholds must be configurable.

Filesystem-specific exceptions may be stored in metadata.

### Why It Matters

Full filesystems may cause:

- Application failures.
- MQ failures.
- Database failures.
- Logging failures.
- Backup failures.
- Authentication issues.
- Operating-system instability.

### Recommended Next Steps

- Identify recently growing files.
- Review application logs.
- Review core files and dumps.
- Confirm expected growth.
- Expand or clean the filesystem through a separate approved workflow.

---

## Future Checks

## Mksysb Coverage

Verify that every required LPAR has a recent mksysb image.

Future metadata may include:

```yaml
requires_mksysb: true
mksysb_max_age_hours: 48
```

The check should validate freshness, not only file existence.

---

## AIX Error Report

Collect recent errors using a bounded time window.

Example:

```sh
errpt -s <start_time>
```

The workflow should classify errors by:

- PERM.
- TEMP.
- INFO.
- Resource.
- Error identifier.
- Frequency.
- Recency.

Historical errors outside the configured window should not affect current health.

---

## Paging Space

Collect paging-space configuration and utilization.

The evaluation should distinguish:

- Paging-space count.
- Total capacity.
- Active paging use.
- Sustained paging pressure.
- Paging-space devices that are inactive.

A single `lsps -a` result should not be treated as a failure without defined evaluation rules.

---

## Volume Groups

Collect active volume groups and physical-volume state.

Potential checks include:

- Missing physical volumes.
- Stale partitions.
- Inactive volume groups expected to be active.
- Quorum state.
- Mirror consistency.

---

## Dump Device

Validate dump-device configuration and capacity.

The existing script uses:

```sh
/usr/lib/ras/dumpcheck -p
```

The new workflow should record both configured dump devices and any capacity warning.

---

## CPU and Memory

Collect short-duration performance samples.

Potential commands:

```sh
vmstat 1 5
svmon -G
lparstat
```

A single CPU sample should be informational unless thresholds and duration are clearly defined.

Historical performance monitoring should remain separate from an immediate health check.

---

## OS Level

Collect:

```sh
oslevel -s
```

The result is informational unless compared to approved lifecycle metadata.

Example:

```yaml
approved_oslevel: "7200-05-08-2446"
```

---

## Remote Restart

Remote restart readiness is an HMC or PowerVM health check rather than a purely local AIX check.

It may be included in a combined Power/AIX report, but collection should occur through the HMC.

---

## Preferred Frame Placement

Preferred hardware placement should use inventory metadata.

Example:

```yaml
preferred_managed_system: Server-9009-22A-SN787BFE0
```

Hard-coded LPAR lists should not be stored in the health role.

---

## Structured Results

Example NTP result:

```yaml
- id: aix.ntp
  title: NTP Service
  technology: aix
  target: txwcsp11
  status: PASS
  summary: xntpd is active
  meaning: System time synchronization is running.
  why_it_matters: Accurate time is required for logs, authentication, and distributed processing.
  recommendation: ""
  evidence:
    subsystem: xntpd
    state: active
```

Example filesystem result:

```yaml
- id: aix.filesystem.var
  title: Filesystem /var
  technology: aix
  target: txwcsp11
  status: WARN
  summary: /var is 84 percent utilized
  meaning: The filesystem has exceeded the warning threshold.
  why_it_matters: Continued growth may interrupt logging or system services.
  recommendation: Review recent growth and large files under /var.
  evidence:
    mount: /var
    utilization_percent: 84
    warning_percent: 80
    critical_percent: 90
```

---

## Inventory and Configuration

Suggested defaults:

```yaml
aix_health:
  filesystem_warning_percent: 80
  filesystem_critical_percent: 90
  expected_disk_paths_per_disk: 8
  errpt_window_hours: 24
  mksysb_max_age_hours: 48
```

Target overrides should be stored in inventory metadata.

Example:

```yaml
txwcsp11:
  aix_health:
    expected_disk_paths_per_disk: 8
    excluded_filesystems:
      - /proc
```

---

## Error Handling

The workflow must distinguish between:

```text
FAIL
The infrastructure condition is unhealthy.

ERROR
The check could not collect reliable evidence.
```

Examples:

```text
FAIL
xntpd is confirmed inactive.

ERROR
The host could not be reached, so NTP state is unknown.
```

An unreachable host must not produce false failures for every check.

---

## Reporting

The quick view should look similar to:

```text
AIX Health
==========

Host............... txwcsp11
Overall Status..... WARN

PASS NTP Service
     xntpd is active.

PASS Bootlist
     Normal bootlist matches rootvg.

PASS Disk Paths
     All expected storage paths are enabled.

WARN Filesystems
     /var is 84 percent utilized.

Meaning
-------
The host is operational, but /var has exceeded the warning threshold.

Recommended Action
------------------
Review growth under /var before it reaches the critical threshold.
```

Detailed evidence should be stored in the workflow workspace.

---

## Migration Strategy

The existing `health_check.ksh` script should remain available while the new workflow is developed.

Migration stages:

1. Document existing checks.
2. Implement the common health result model.
3. Build initial AIX collection.
4. Compare new results with the existing script.
5. Validate across multiple LPARs.
6. Add missing checks incrementally.
7. Generate equivalent or improved reporting.
8. Retire the old script only after operational validation.

The existing script is a reference implementation and should not be removed prematurely.
