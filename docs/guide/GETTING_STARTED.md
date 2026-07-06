# Getting Started

Welcome to the Power Infrastructure project.

Power Infrastructure is an engineering platform for managing IBM Power environments through inventory, validation, documentation, reporting, and automation.

Rather than maintaining scripts, spreadsheets, and documentation independently, the project aims to generate operational knowledge from a single authoritative inventory.

---

# Project Goals

The long-term objectives of the project include:

- Automated inventory collection
- Configuration validation
- Generated documentation
- Operational reporting
- Disaster recovery automation
- LPAR lifecycle management
- User administration
- Backup and restore automation
- Patch management
- Environment health reporting

---

# Engineering Principles

Development throughout the project follows several core principles.

## Single Source of Truth

Inventory data should be collected from trusted systems and become the authoritative source for documentation, reports, and automation.

## Generate Before Deploy

Automation should generate proposed actions before making changes whenever practical.

## Validate Before Execute

Operational workflows should verify prerequisites before executing changes.

## Documentation Should Be Generated

Documentation should be produced automatically whenever possible rather than maintained manually.

## Small Reusable Components

Utilities should perform one task well and be reusable throughout larger workflows.

## Pipelines Instead of Procedures

Manual checklists should gradually evolve into validated automation pipelines.

Typical workflow:

Inventory

↓

Validation

↓

Metadata Merge

↓

Documentation

↓

Review

↓

Automation

↓

Verification

---

# Project Layout

The repository is organized into functional areas.

```
docs/
inventory/
playbooks/
roles/
scripts/
tools/
```

Documentation explains how the project works.

Inventory contains collected and generated environment data.

Playbooks orchestrate operational workflows.

Roles implement reusable automation components.

Scripts provide supporting utilities.

Tools provide the command-line interface used throughout the project.

---

# Development Workflow

A typical engineering task follows this progression.

1. Understand the manual process.
2. Document the workflow.
3. Build inventory collection.
4. Build validation.
5. Generate reports.
6. Review proposed changes.
7. Automate execution.
8. Verify results.
9. Generate completion documentation.

---

# Documentation

Documentation is organized by purpose.

- Guide
- Planning
- Design
- Reference
- Generated
- Runbooks
- Session Updates

Each section serves a different purpose and should be updated as the project evolves.

---

# Where to Start

If you are contributing to the project for the first time, read:

1. Architecture
2. Session Workflow
3. Documentation Standards
4. PWR CLI

These documents explain how engineering work is performed within the project.
