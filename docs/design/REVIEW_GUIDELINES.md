# Operational Review Development Guidelines

## Purpose

This document defines engineering standards for developing Operational Reviews within the Power Infrastructure project.

The goal is to ensure every review follows a consistent structure, produces predictable output, and remains easy to understand, maintain, and extend.

These guidelines complement the Operational Review Framework by describing implementation standards rather than architectural concepts.

---

# Guiding Principles

Operational Reviews should be:

- read-only
- deterministic
- repeatable
- easy to troubleshoot
- reusable
- well documented

A review should produce the same conclusions when executed repeatedly against an unchanged environment.

---

# Single Responsibility

Each review should answer a single engineering question.

Examples:

- Is IBM MQ healthy?
- Are filesystems healthy?
- Is the HMC healthy?
- Is backup protection healthy?

Avoid creating reviews that attempt to assess the entire environment.

Large assessments should combine multiple reviews rather than expanding individual reviews.

---

# Review Stages

Every review should follow the standard lifecycle.

```text
Initialize
Collect
Validate
Analyze
Summarize
Report
```

Each stage should have a clear responsibility.

---

## Initialize

Responsible for:

- loading configuration
- validating arguments
- loading inventory
- recording metadata

Do not collect operational data here.

---

## Collect

Collect facts only.

Examples:

Good:

- run dspmq
- run lssrc
- query Pure API
- read inventory

Avoid:

- determining health
- generating recommendations
- interpreting results

Collection should remain objective.

---

## Validate

Validation evaluates collected information.

Validation answers questions such as:

- Is this running?
- Does this meet policy?
- Does this exceed thresholds?

Validation should avoid producing operator recommendations.

---

## Analyze

Analysis converts validation into engineering findings.

Analysis should explain:

- why something matters
- operational impact
- possible risks

Analysis should not repeat raw command output unnecessarily.

---

## Summarize

The summary should communicate the operational state in a few seconds.

A good summary allows an experienced engineer to determine whether further investigation is required.

---

## Report

Reports should preserve sufficient information to:

- understand findings
- reproduce conclusions
- support audits
- prepare change activities

Reports should avoid excessive raw command output unless needed as evidence.

---

# Finding Standards

Every finding should contain:

- status
- summary

Whenever practical, include:

- source
- target
- recommendation
- evidence

Summaries should be concise.

Good:

```text
PASS Queue Manager TXWCSP11 is running.
```

Poor:

```text
PASS
```

---

# Status Definitions

PASS

Requirement satisfied.

WARN

Attention required.

FAIL

Requirement not satisfied.

INFO

Context only.

UNKNOWN

Unable to determine status.

---

# Recommendations

Recommendations should be actionable.

Good:

```text
Investigate queue depth before production processing begins.
```

Avoid vague recommendations.

Poor:

```text
Check MQ.
```

---

# Thresholds

Avoid hardcoding operational thresholds.

Thresholds should eventually reside in centralized configuration.

Examples include:

- filesystem usage
- queue depth
- replication lag
- CPU utilization

---

# Console Output

Console output should prioritize readability.

Preferred order:

```text
Summary

PASS/WARN/FAIL

Key Findings

Recommendations

Additional Details
```

Avoid overwhelming operators with unnecessary detail.

---

# Generated Reports

Markdown reports should contain:

- title
- target
- execution time
- summary
- findings
- recommendations
- evidence
- project version

Reports should be reproducible.

---

# Error Handling

Reviews should fail gracefully.

If data cannot be collected:

- report UNKNOWN
- explain why
- continue collecting remaining information whenever practical

Avoid terminating the entire review because one check failed.

---

# Logging

Reviews should record enough information for troubleshooting.

Logs should distinguish between:

- collection failures
- validation failures
- operational findings

---

# Performance

Reviews should minimize execution time.

Avoid collecting unnecessary information.

Expensive operations should be clearly documented.

---

# Reusability

Whenever practical:

- reuse collectors
- reuse validators
- reuse reporting
- reuse summary generation

Avoid duplicating implementation logic.

---

# Documentation

Every new review should include:

- purpose
- supported targets
- required inputs
- generated outputs
- known limitations

---

# Naming Conventions

Review names should describe the engineering domain.

Preferred:

- mq
- filesystem
- backup
- pure
- hmc
- aix
- vios

Avoid implementation-specific names.

Poor:

- mq-health-v2
- queuecheck
- servicecheck

---

# Testing

Every review should be validated using:

- healthy environment
- warning condition
- failure condition

Expected results should be documented.

---

# Backward Compatibility

Existing production workflows should remain functional whenever practical.

Framework improvements should avoid unnecessary disruption.

---

# Engineering Philosophy

Operational Reviews exist to improve understanding of the environment.

They do not make changes.

They provide trusted engineering assessments that support planning, troubleshooting, auditing, and future automation.

Automation begins after understanding.

Operational Reviews establish that understanding.
