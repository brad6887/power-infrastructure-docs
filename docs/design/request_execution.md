# Request Execution Framework

## Purpose

The Request Execution Framework defines how operational requests are executed within the Power Infrastructure platform.

Rather than invoking Ansible playbooks directly, operators execute requests through the `pwr` command-line interface. The framework is responsible for loading request metadata, initializing the Workflow Engine, selecting the appropriate workflow, executing automation, and generating operational documentation.

The objective is to provide a consistent execution model for every operational workflow.

---

# Goals

The framework should:

- Eliminate manual Ansible command construction.
- Standardize workflow execution.
- Initialize the Workflow Engine automatically.
- Generate documentation for every execution.
- Produce consistent reports and artifacts.
- Support validation, planning, execution, and verification.
- Capture operational history.

---

# High-Level Workflow

```
Operator
    │
    ▼
pwr request run REQ0722461
    │
    ▼
Load Request Metadata
    │
    ▼
Select Workflow
    │
    ▼
Initialize Workflow Engine
    │
    ▼
Workflow Preparation
    │
    ▼
Validation
    │
    ▼
Plan
    │
    ▼
Execute
    │
    ▼
Verify
    │
    ▼
Report
    │
    ▼
Generate Documentation
    │
    ▼
Archive Results
```

---

# Request Workspace

Every operational request is represented by a request workspace.

Example:

```
requests/
    REQ0722461/
        request.yml
        ssh_key.pub
        attachments/
```

Generated artifacts are stored separately:

```
docs/generated/requests/
    REQ0722461/
        workflow_summary.md
        validation.md
        execution.md
        verification.md
```

This separation keeps source request data independent from generated output.

---

# Request Metadata

Each request is described by `request.yml`.

Example:

```yaml
id: REQ0722461

workflow: add-user

targets:
  - txedip11
  - txedit11

users:
  - username: ShivaniB
```

The metadata becomes the authoritative input for workflow execution.

---

# Workflow Context

The Request Execution Framework initializes a standard `workflow_context`.

Example:

```yaml
workflow_context:
  request_id:
  operator:
  started_at:
  mode:
  stage:
  status:
  workspace:
  artifacts:
```

Every Workflow Engine stage receives and updates this shared context.

---

# Workflow Selection

The request metadata determines which workflow is executed.

Example:

```
workflow: add-user
```

becomes

```
playbooks/users/add_user.yml
```

Operators should not need to know playbook names.

---

# Command-Line Interface

The intended operator interface is:

```bash
pwr request run REQ0722461
```

The CLI is responsible for:

- locating the request
- loading metadata
- selecting the workflow
- building the execution context
- launching the workflow
- presenting progress
- generating documentation

---

# Workflow Responsibilities

The Workflow Engine performs all execution responsibilities.

```
workflow_prepare
workflow_validate
workflow_plan
workflow_execute
workflow_verify
workflow_report
workflow_document
workflow_archive
```

Operational workflows should focus only on business logic.

---

# Reporting

Every execution should produce a consistent set of artifacts.

Examples:

- Workflow summary
- Validation report
- Execution report
- Verification report
- Communications
- Completion summary

---

# Long-Term Vision

The Request Execution Framework becomes the standard execution model for every operational capability.

Examples include:

- User Administration
- Backup Operations
- Restore Operations
- Inventory Collection
- Patch Management
- LPAR Lifecycle
- Disaster Recovery

The operator experience should remain consistent regardless of the workflow being executed.

Ultimately, engineers should execute operational work through requests rather than directly invoking playbooks, allowing the platform to provide validation, reporting, documentation, and historical tracking automatically.
