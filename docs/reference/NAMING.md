# Naming Standards

This document defines naming standards used throughout the Power Infrastructure project.

Consistent names make inventory, documentation, reports, and automation easier to understand and maintain.

---

# General Principles

Names should be:

- clear
- consistent
- predictable
- descriptive
- automation-friendly

Avoid names that require tribal knowledge whenever practical.

---

# Repository Naming

Use lowercase directory names.

Examples:

```text
docs/
inventory/
playbooks/
roles/
scripts/
tools/
```

Use uppercase filenames for major planning and reference documents.

Examples:

```text
PROJECT_STATUS.md
BACKLOG.md
ROADMAP.md
MILESTONES.md
DIRECTORY_LAYOUT.md
STANDARDS.md
NAMING.md
```

Use lowercase hyphenated filenames for dated journal entries and session updates.

Examples:

```text
2026-07-06-documentation-standardization.md
2026-07-06-user-workflow.md
```

---

# Documentation Naming

Document names should describe the purpose of the file.

Good examples:

```text
SESSION_WORKFLOW.md
DOCUMENTATION.md
PWR_CLI.md
PLANNING_SCHEMA.md
```

Avoid vague names such as:

```text
notes.md
misc.md
stuff.md
updates.md
```

---

# Ansible Role Naming

Role names should describe the function they perform.

Examples:

```text
aix_user_prepare_add
aix_user_validate_add
aix_user_add
aix_user_report

aix_user_validate_remove
aix_user_remove

veeam_session_validate
```

Preferred pattern:

```text
platform_subject_action
```

Examples:

```text
aix_user_add
aix_user_remove
aix_user_validate_add
veeam_restore_plan
hmc_inventory_collect
```

---

# Playbook Naming

Playbook names should describe the workflow they execute.

Examples:

```text
add_user.yml
remove_user.yml
restore_backup.yml
collect_hmc_inventory.yml
```

Playbooks should be grouped by operational area when practical.

Examples:

```text
playbooks/users/add_user.yml
playbooks/users/remove_user.yml
playbooks/backup/restore_backup.yml
```

---

# Generated Request Naming

Generated request documentation should include the request or ticket number when available.

Examples:

```text
docs/generated/requests/REQ0722461/
docs/generated/requests/REQ0720991/
```

This keeps request-specific output grouped and easy to locate.

---

# Variable Naming

Variables should be descriptive and predictable.

Use lowercase words separated by underscores.

Examples:

```text
target_user
source_user
request_number
ssh_public_key
home_directory
primary_group
```

Avoid unclear abbreviations unless they are well-known in the environment.

---

# Command Naming

Project commands should be short and task-oriented.

Examples:

```text
pwr doctor
pwr publish docs
pwr session
```

Command names should describe the user's intent rather than the implementation detail.

---

# Long-Term Goal

Naming should support automation.

A consistent naming standard makes it easier to build tooling that can discover files, generate documentation, validate workflows, and guide engineers through repeatable processes.
