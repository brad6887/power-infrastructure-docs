# Power Infrastructure Philosophy

## Purpose

The goal of this project is to build an engineering platform rather than a collection of scripts.

Every component should contribute toward creating repeatable, reliable, and understandable operational workflows.

---

# Guiding Principles

## Authoritative Sources of Truth

Enterprise environments rarely have a single source of truth.

Instead, each system is authoritative for the information it owns.

Examples include:

| Information        | Authoritative Source |
| ------------------ | -------------------- |
| IBM Power hardware | HMC                  |
| LPAR configuration | HMC                  |
| Storage            | Pure Storage         |
| Backup             | Veeam                |
| Business metadata  | Project metadata     |

The project combines these authoritative sources into a normalized inventory rather than manually maintaining duplicate information.

---

## Validate Before Generating

Infrastructure data should be validated before documentation, reports, or automation are generated.

Errors should be identified as early as possible.

---

## Generate Rather Than Maintain

Documentation should be generated whenever practical.

Generated documentation is more accurate, more consistent, and easier to maintain than manually edited documents.

---

## Small Purpose-Built Tools

Each utility should perform one task well.

Examples include:

* Import inventory
* Validate inventory
* Compare inventory
* Generate reports
* Generate documentation
* Execute automation

Complex workflows should be built by combining small tools rather than creating large monolithic applications.

---

## Automation Follows Understanding

Automation should be built on validated infrastructure data.

Reliable inventory and documentation should exist before operational automation is introduced.

---

## Pipelines Over Procedures

Operational processes should become repeatable workflows.

Example:

Authoritative Data

↓

Import

↓

Validation

↓

Normalized Inventory

↓

Documentation

↓

Reports

↓

Automation

↓

Verification

---

## Production First

This project is intended for enterprise production environments.

Reliability, maintainability, and operational safety take precedence over experimentation.

Ideas may be developed elsewhere before being incorporated into this project.

---

## Success Criteria

Success is measured by:

* Reduced manual effort
* Improved documentation accuracy
* Repeatable operational workflows
* Reliable infrastructure inventory
* Faster environment understanding
* Safer infrastructure changes
* Better operational visibility
* Increased automation built on trusted data


---

## Target Runtime

Power Infrastructure should remain compatible with the enterprise automation environment.

The primary automation server currently uses Python 3.6, so Python scripts should avoid features that require newer Python versions unless there is a clear reason to raise the runtime requirement.

Prefer Python 3.6-compatible patterns for enterprise reliability and portability.
