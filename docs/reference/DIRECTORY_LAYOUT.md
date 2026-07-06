# Directory Layout

This document describes the organization of the Power Infrastructure repository.

Directories are organized by function to keep inventory, automation, documentation, and tooling clearly separated.

---

# Top-Level Layout

```
docs/
inventory/
playbooks/
roles/
scripts/
tools/
```

Each directory has a single primary responsibility.

---

# docs/

Project documentation.

```
docs/

├── guide/
├── planning/
├── design/
├── reference/
├── generated/
├── runbooks/
└── session-updates/
```

### guide

Project usage and engineering workflow documentation.

### planning

Current project status, roadmap, backlog, milestones, and priorities.

### design

Architecture and engineering design documents.

### reference

Stable project reference material.

### generated

Automatically generated documentation.

### runbooks

Operational procedures.

### session-updates

Summaries of completed engineering sessions.

---

# inventory/

Infrastructure inventory.

```
inventory/

source/
generated/
metadata/
```

### source

Collected data from infrastructure.

### generated

Processed inventory used by documentation and automation.

### metadata

Administrative information that supplements collected inventory.

---

# playbooks/

Top-level Ansible playbooks.

Playbooks orchestrate complete operational workflows.

Examples include:

- User administration
- Backup restore
- Patch management
- Disaster recovery

---

# roles/

Reusable Ansible roles.

Roles should perform one well-defined task.

Complex workflows should be composed from multiple small roles.

---

# scripts/

Supporting utilities.

Scripts should perform focused tasks that are reused throughout the project.

---

# tools/

Project tooling.

Examples include:

- pwr
- build utilities
- documentation generators
- validation utilities
- inventory collectors

---

# Design Guidelines

When adding new content:

- Place it in the directory matching its purpose.
- Avoid duplicate information.
- Favor reusable components.
- Keep generated content separate from manually maintained documentation.
- Organize for long-term maintainability rather than short-term convenience.

The repository structure should support the engineering workflow rather than dictate it.
