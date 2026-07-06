# Power Infrastructure Documentation

Welcome to the Power Infrastructure documentation.

Power Infrastructure is an enterprise automation and operations framework for IBM Power environments. The project combines inventory collection, validation, documentation generation, reporting, and automation into a single engineering platform designed to improve operational consistency and reduce manual effort.

The documentation is organized by purpose so engineers can quickly locate planning information, operational guidance, generated reports, and reference material.

---

# Start Here

If you are new to the project, read these documents in order.

- Getting Started
- Architecture
- Session Workflow
- Documentation Standards
- PWR CLI

These guides explain how the project is organized, how work is performed, and how documentation and automation fit together.

---

# Planning

Planning documents describe the current state of the project and its future direction.

- Project Status
- Next
- Backlog
- Roadmap
- Milestones

These documents should be updated throughout the life of the project and represent the current engineering priorities.

---

# Design

Design documents describe the architecture and engineering decisions behind the project.

Examples include:

- Workflow Engine
- Inventory Architecture
- Documentation Generation
- Validation Framework
- Automation Design

Design documentation explains *why* components are built the way they are before describing implementation details.

---

# Reference

Reference documentation contains information that changes infrequently and serves as the project's long-term knowledge base.

Examples include:

- Directory Layout
- Naming Standards
- Coding Standards
- HMC Reference
- VIOS Reference
- Pure Storage Reference
- Veeam Reference

As the project grows, additional reference documentation will be added here.

---

# Generated Documentation

Generated documentation is produced automatically from inventory data whenever practical.

Examples include:

- Environment summaries
- Inventory reports
- Capacity reports
- Validation reports
- Disaster recovery documentation

Generated documents should not be manually edited. Instead, update the source data or generation process and rebuild the documentation.

---

# Runbooks

Runbooks document repeatable operational procedures.

Examples include:

- User administration
- Backup restores
- Disaster recovery
- Patch management
- LPAR deployment
- LPAR decommissioning

Where possible, runbooks should evolve into validated automation workflows while remaining useful as operational documentation.

---

# Session Updates

Session updates provide lightweight summaries of individual work sessions.

Each update captures:

- what was accomplished
- significant design decisions
- documentation changes
- impact on the project

During periodic documentation reviews, completed session updates should be reconciled into the project's planning and reference documentation.

---

# Project Philosophy

Power Infrastructure follows several core engineering principles.

- Maintain a single source of truth through generated inventory.
- Validate before executing automation.
- Generate proposed plans before making changes.
- Produce documentation whenever practical.
- Build small, reusable components.
- Prefer repeatable workflows over manual procedures.

These principles guide both the architecture of the project and the automation developed within it.
