# User Workflow Mapping

This document maps the current User Administration workflow to the future Workflow Engine architecture.

The purpose is to identify which parts of the current implementation are workflow-specific and which parts should eventually become reusable Workflow Engine components.

---

# Current Add User Workflow

```text
playbooks/users/add_user.yml

    ↓

Common preparation

    ↓

User-specific preparation

    ↓

Validation

    ↓

Plan / Execute

    ↓

Verification

    ↓

Report
```

---

# Current Remove User Workflow

```text
playbooks/users/remove_user.yml

    ↓

Common preparation

    ↓

User-specific preparation

    ↓

Validation

    ↓

Plan / Execute

    ↓

Verification

    ↓

Report
```

---

# Current Role Mapping

| Current Component | Current Purpose | Future Engine Stage |
|-------------------|-----------------|---------------------|
| `playbooks/users/add_user.yml` | Orchestrates add-user workflow | Workflow entry point |
| `playbooks/users/remove_user.yml` | Orchestrates remove-user workflow | Workflow entry point |
| `aix_user_prepare` | Common user preparation | Candidate for `workflow_prepare` |
| `aix_user_prepare_add` | Add-user specific preparation | Workflow-specific preparation |
| `aix_user_validate` | Common user validation | Candidate for `workflow_validate` |
| `aix_user_validate_remove` | Remove-user validation | Workflow-specific validation |
| `aix_user_add` | Executes user creation | Workflow-specific execution |
| `aix_user_remove` | Executes user removal | Workflow-specific execution |
| `aix_user_verify` | Verifies user state | Candidate for `workflow_verify` with user-specific checks |
| `aix_user_report` | Generates user workflow report | Candidate for `workflow_report` |

---

---

# Current Implementation Inventory

## Playbooks

| File | Purpose | Notes |
|------|---------|-------|
| `playbooks/users/add_user.yml` | Main add-user workflow | Primary reference workflow |
| `playbooks/users/remove_user.yml` | Main remove-user workflow | In progress |
| `playbooks/users/aix_user_add_plan.yml` | Add-user planning workflow | Candidate to merge into standard plan mode |
| `playbooks/users/inspect_aix_user.yml` | User inspection workflow | Useful for validation and verification |

## Roles

| Role | Purpose | Future Classification |
|------|---------|----------------------|
| `aix_user_prepare` | Common user preparation | Candidate for generic workflow preparation |
| `aix_user_prepare_add` | Add-user preparation | User workflow-specific preparation |
| `aix_user_validate` | Common user validation | Candidate for generic validation pattern |
| `aix_user_validate_remove` | Remove-user validation | User workflow-specific validation |
| `aix_user_create` | User creation execution | User workflow-specific execution |
| `aix_user_remove` | User removal execution | User workflow-specific execution |
| `aix_user_ssh` | SSH key management | User workflow-specific execution component |
| `aix_user_verify` | User verification | Candidate for generic verification pattern |
| `aix_user_report` | User report generation | Candidate for generic reporting pattern |
| `aix_user_inspect` | Inspect existing user state | Reusable user-specific support role |

## Common Tasks

| Task | Purpose | Future Classification |
|------|---------|----------------------|
| `common/tasks/check_user_exists.yml` | Checks whether a user exists | Reusable validation task |
| `common/tasks/normalize_username.yml` | Normalizes username input | Reusable preparation task |
| `common/tasks/validate_username.yml` | Validates username format | Reusable validation task |

# Candidate Generic Responsibilities

These responsibilities appear reusable across future workflows.

## Workflow Prepare

- Load request metadata.
- Identify operator.
- Set execution timestamp.
- Define workspace path.
- Create generated artifact directories.
- Load inventory context.
- Set execution mode.

## Workflow Validate

- Collect validation results.
- Standardize passed / warning / failed output.
- Stop execution on validation failures.
- Preserve validation artifacts.

## Workflow Plan

- Generate proposed actions.
- Support plan-only mode.
- Preserve plan output.

## Workflow Execute

- Track changed state.
- Capture task results.
- Preserve execution output.

## Workflow Verify

- Run post-execution checks.
- Capture verification results.
- Standardize passed / warning / failed output.

## Workflow Report

- Generate Markdown reports.
- Include request metadata.
- Include validation results.
- Include execution results.
- Include verification results.

---

# Workflow-Specific Responsibilities

These responsibilities should remain specific to User Administration.

## Add User

- Normalize target username.
- Compare to source user.
- Determine primary and secondary groups.
- Determine home directory.
- Install SSH public keys.
- Create account.
- Verify account state.

## Remove User

- Confirm target user exists.
- Validate removal safety.
- Remove or disable account.
- Handle home directory policy.
- Verify account removal or disabled state.

---

# Migration Strategy

The User Administration workflow will remain the reference implementation for the Workflow Engine.

Migration should be incremental.

1. Document the current workflow.
2. Identify reusable behavior.
3. Extract common preparation into `workflow_prepare`.
4. Standardize validation output.
5. Standardize reporting output.
6. Update the add-user workflow to consume generic workflow stages.
7. Update the remove-user workflow to consume generic workflow stages.
8. Apply lessons learned before migrating backup, restore, patch management, inventory, and disaster recovery workflows.

---

# Open Questions

- Should Workflow Engine roles live under `roles/workflow_*` or `roles/workflow/<stage>`?
- Should the workflow context be written to a YAML artifact?
- Should every workflow generate both JSON and Markdown output?
- Should `pwr workflow` become the primary entry point for all engine-based workflows?
- Which responsibilities belong in Ansible roles versus Python utilities?

---

# Preparation Finding

The current `aix_user_prepare` role performs common User Administration preparation, not generic workflow preparation.

It prepares normalized AIX user objects by applying reference-user defaults, group logic, home directory defaults, shell defaults, and SSH key metadata.

This role should remain part of the User Administration workflow.

A future generic `workflow_prepare` role should be created separately to handle workflow-level context such as:

- request metadata
- operator
- timestamp
- execution mode
- workspace path
- artifact directories
- inventory context

This confirms that workflow preparation and workflow-specific preparation are separate stages.

---

# Add-User Preparation Finding

The `aix_user_prepare_add` role performs add-user-specific preparation.

It enriches prepared user records with SSH public key data from the request workspace.

This role should remain part of the User Administration workflow and should not become part of the generic Workflow Engine.

The role confirms that workflow-specific preparation may occur after common workflow preparation and before validation.


---

# Add-User Playbook Finding

The current `add_user.yml` playbook is already structured as a simple role pipeline.

This makes it a good reference implementation for the Workflow Engine.

The future generic `workflow_prepare` role should be inserted before `aix_user_prepare`.

Current flow:

```text
aix_user_prepare
    ↓
aix_user_prepare_add
    ↓
aix_user_validate
    ↓
aix_user_create
    ↓
aix_user_ssh
    ↓
aix_user_verify
    ↓
aix_user_report
    ↓
communications

---

# Workflow Prepare Prototype

A first generic `workflow_prepare` role has been created and tested.

The role currently handles:

- workflow timestamp
- workflow operator
- request id
- workflow mode
- normalized workflow workspace path
- workspace creation
- workflow context object

Test playbook:

```text
playbooks/workflow/test_prepare.yml

---

# Add-User Integration Test

The generic `workflow_prepare` role was inserted into `playbooks/users/add_user.yml` before the User Administration preparation roles.

A test run against `localhost` confirmed that:

- `workflow_prepare` runs first.
- `workflow_context` is created.
- `aix_user_prepare` still builds prepared user records.
- `aix_user_prepare_add` still enriches prepared user records.
- Validation proceeds normally.

The test failed during shell validation because `localhost` is a Linux system and does not contain `/usr/bin/ksh`.

This confirms that the Workflow Engine integration did not break the user preparation pipeline.
