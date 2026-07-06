# Documentation Standards

Power Infrastructure documentation should be clear, current, and organized by purpose.

The goal is to make the project easy to understand, easy to resume, and easy to operate.

---

# Documentation Principles

## Documentation Is Part of the Workflow

Documentation should be updated as engineering work is completed.

If a workflow, tool, command, inventory source, or project priority changes, the related documentation should be reviewed.

## Generated Before Manual

Documentation should be generated from inventory and source data whenever practical.

Manual documentation should explain process, design, and intent.

Generated documentation should describe the current environment state.

## Source Data First

When generated documentation is incorrect, fix the source data or generation logic rather than manually editing the generated output.

## Keep Documents Focused

Each document should have a clear purpose.

Avoid turning one document into a catch-all for unrelated notes.

---

# Documentation Areas

## Guide

Guides explain how to use and work within the project.

Examples:

- Getting Started
- Architecture
- Session Workflow
- Documentation Standards
- PWR CLI

## Planning

Planning documents describe current status, priorities, backlog, milestones, and roadmap.

Examples:

- Project Status
- Next
- Backlog
- Roadmap
- Milestones

## Design

Design documents describe architecture, workflows, and engineering decisions.

Examples:

- Workflow Engine
- Inventory Design
- Validation Design
- Documentation Generation

## Reference

Reference documents contain stable project knowledge.

Examples:

- Directory Layout
- Naming Standards
- Coding Standards
- HMC Reference
- VIOS Reference
- Veeam Reference

## Generated

Generated documents are produced by project tooling.

Examples:

- Environment Summary
- Inventory Reports
- Validation Reports
- Capacity Reports

## Runbooks

Runbooks describe repeatable operational procedures.

Examples:

- User Administration
- Backup Restore
- Patch Management
- Disaster Recovery
- LPAR Deployment

## Session Updates

Session updates capture work completed during individual sessions.

They provide a lightweight history that can later be reconciled into planning, design, or reference documentation.

---

# Generated Documentation Rules

Generated documentation should include a note indicating that it is generated.

Generated files should not be manually edited.

If generated output is wrong:

1. Correct the inventory source.
2. Correct metadata.
3. Correct the generator.
4. Rebuild the document.

---

# Session Documentation

At the end of a meaningful work session, create a session update.

A session update should include:

- Summary
- Completed work
- Design decisions
- Operational impact
- Follow-up items

Session updates should be reviewed periodically and folded into long-term documentation where appropriate.

---

# Naming Conventions

Use uppercase filenames for major planning and reference documents.

Examples:

```text
PROJECT_STATUS.md
BACKLOG.md
ROADMAP.md
DIRECTORY_LAYOUT.md
```

Use lowercase hyphenated filenames for dated journal or session-update files.

Examples:

```text
2026-07-06-documentation-standardization.md
2026-07-06-user-workflow.md
```

---

# Review Cadence

Documentation should be reviewed:

- at the end of each work session
- before commits
- after major workflow changes
- after generated inventory changes
- during periodic project review sessions

The documentation should always reflect the current direction of the project.
