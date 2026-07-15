## Operational Health Framework

The Operational Health framework continued to mature into a reusable operational review platform built on the standard Workflow Engine.

Rather than creating standalone diagnostic scripts, Operational Health workflows follow the common execution lifecycle:

```text
Prepare
↓
Validate
↓
Collect
↓
Evaluate
↓
Quick View
↓
Report
↓
Structured Results
```

Recent enhancements include:

* Modular evidence collection roles
* Modular evaluation roles
* Host-specific artifact workspaces
* Fleet operational review support
* Fleet summary generation
* Standardized Markdown reports
* Standardized JSON results
* Generic quick-view summaries

Current AIX operational review coverage includes:

* Operating system validation
* NTP validation
* Paging space utilization
* Memory utilization summary
* CPU utilization summary
* Network validation
* Bootlist validation
* Boot device validation
* Dump device validation
* Disk path validation
* Filesystem capacity
* AIX error report analysis

Reference implementations currently include:

* MQ Operational Health
* AIX Operational Health

The framework now supports both single-host operational reviews and inventory group reviews using the same workflow architecture. Each reviewed host generates independent artifacts which can then be aggregated into fleet-level operational summaries.

This architecture establishes the foundation for future Operational Health workflows covering Pure Storage, VIOS, HMC, Oracle, Veeam, networking, and additional infrastructure technologies.
