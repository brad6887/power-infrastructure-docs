# Workflow Engine

## Purpose

The Workflow Engine defines the standard execution model for all operational workflows within Power Infrastructure.

Rather than implementing independent automation for each operational task, every workflow follows a common engineering pipeline.

This ensures consistent validation, reporting, documentation, and operational behavior across the project.

---

# Goals

The Workflow Engine should provide:

- A consistent execution model
- Standard workflow stages
- Reusable automation components
- Standard reporting
- Standard documentation
- Common metadata
- Common validation
- Common error handling

Operational workflows should differ only in their workflow-specific logic.

---

# Workflow Lifecycle

Every workflow follows the same lifecycle.

```
Request
    ↓
Prepare
    ↓
Workflow Preparation
    ↓
Validate
    ↓
Plan
    ↓
Execute
    ↓
Verify
    ↓
Report
    ↓
Documentation
    ↓
Archive
```

Each stage has a single responsibility.

---

# Workflow Stage Model

Each workflow stage has a defined responsibility.

A stage should:

- accept known inputs
- perform one logical function
- produce standard outputs
- avoid duplicating another stage's responsibility

---

# Engine Responsibility

The Workflow Engine is responsible for orchestration.

The engine should:

- load request metadata
- initialize the workflow context
- run workflow stages in order
- stop execution on validation failures
- collect results
- generate reports
- preserve artifacts

The engine should not contain workflow-specific business logic.

Workflow-specific logic belongs in reusable roles, scripts, or modules.

---

# Workflow Responsibility

Each workflow provides the logic required for a specific operational task.

Examples:

- Add user
- Remove user
- Restore backup
- Deploy LPAR
- Patch AIX
- Perform DR recovery

A workflow should define:

- required inputs
- preparation logic
- validation rules
- planned actions
- execution steps
- verification checks
- reporting data

---

# Stage 1 - Request

## Purpose

Capture the reason the workflow exists.

A request may originate from:

- service request
- incident
- change
- manual engineering task

## Inputs

- request number
- request type
- requester
- operator
- target systems
- workflow type
- request text

## Outputs

- request workspace
- request metadata
- request status

Example:

```yaml
request:
  id: REQ0722461
  type: user_add
  status: open
  owner: bcooke
  workflow: aix_user_add
```

---

# Stage 2 - Prepare

## Purpose

Build the common workflow context used by all workflows.

This stage is shared across workflows.

## Inputs

- request metadata
- project configuration
- inventory
- operator information
- runtime options

## Outputs

- workflow context
- workspace paths
- timestamp metadata
- inventory context

Example:

```yaml
workflow:
  name: aix_user_add
  mode: plan
  operator: bcooke
  started_at: 2026-07-06T11:00:00
  workspace: docs/generated/requests/REQ0722461
```

---

# Stage 3 - Workflow Preparation

## Purpose

Build workflow-specific objects.

This stage translates request data into structured objects the workflow can use.

## Examples

User workflow:

```yaml
prepared_user:
  username: shivanib
  source_user: santoshb
  target_hosts:
    - txedip11
    - txedit11
```

Backup restore workflow:

```yaml
restore_request:
  source_host: txwcsp11
  restore_point: latest
  target_path: /restore
```

---

# Stage 4 - Validate

## Purpose

Determine whether the workflow can safely continue.

Validation should happen before execution.

## Outputs

```yaml
validation:
  passed: true
  warnings: []
  failures: []
```

Validation failures should stop execution unless explicitly overridden.

---

# Stage 5 - Plan

## Purpose

Generate the proposed actions before making changes.

The plan stage should describe what will happen.

It should not change systems.

## Outputs

```yaml
plan:
  actions:
    - Create user shivanib
    - Create home directory
    - Install SSH public key
    - Verify login configuration
```

---

# Stage 6 - Execute

## Purpose

Perform the approved changes.

Execution should consume the prepared context and generated plan.

## Outputs

```yaml
execution:
  changed: true
  results:
    - task: create_user
      changed: true
      status: success
```

---

# Stage 7 - Verify

## Purpose

Confirm the requested changes completed successfully.

Verification proves the workflow achieved its intended result.

## Outputs

```yaml
verification:
  passed: true
  checks:
    - user_exists
    - home_directory_exists
    - ssh_key_installed
```

---

# Stage 8 - Report

## Purpose

Generate a standard workflow report.

Reports should include:

- request metadata
- workflow metadata
- validation results
- planned actions
- execution results
- verification results

---

# Stage 9 - Documentation

## Purpose

Generate durable project documentation from the workflow results.

Examples:

- request summary
- execution report
- validation report
- completion documentation

---

# Stage 10 - Archive

## Purpose

Close the workflow lifecycle.

Archive should preserve:

- request metadata
- generated reports
- execution output
- validation results
- verification results

---

# Workflow Contract

Every workflow must expose the same interface to the Workflow Engine.

The engine should never need to know the details of a workflow.

Instead, each workflow implements the standard stages defined by the engine.

```
Workflow Engine
        │
        ├── Prepare
        ├── Workflow Preparation
        ├── Validate
        ├── Plan
        ├── Execute
        ├── Verify
        ├── Report
        ├── Documentation
        └── Archive
```

The Workflow Engine invokes these stages in order.

Each workflow is responsible only for implementing its own business logic.

---

# Required Workflow Components

Every workflow should provide:

- workflow metadata
- preparation
- validation
- planning
- execution
- verification
- reporting
- documentation

Optional stages may be omitted when appropriate.

---

# Workflow Metadata

Each workflow should define metadata describing its capabilities.

Example:

```yaml
workflow:
  name: aix_user_add
  description: Create an AIX user
  supports:
    - plan
    - execute
    - verify
    - report
```

The Workflow Engine can use this metadata to determine supported features.

---

# Workflow Context

The Workflow Engine maintains a shared workflow context.

Each stage receives the current context and may extend it.

Example:

```yaml
request:
workflow:
inventory:
prepared:
validation:
plan:
execution:
verification:
report:
```

Stages should add information rather than replacing existing data.

The workflow context becomes the single source of truth for workflow execution.

---

# Error Handling

Each stage returns one of three results.

Success

The next stage may execute.

Warning

Execution may continue but warnings should be reported.

Failure

Execution stops unless explicitly overridden.

---

# Idempotency

Every workflow should be idempotent whenever practical.

Running a completed workflow a second time should produce no unnecessary changes.

Verification should demonstrate that the desired state already exists.

---

# Extensibility

The Workflow Engine should allow new workflows to be added without modifying the engine itself.

Adding a new workflow should require:

- workflow metadata
- stage implementations
- workflow registration

The engine should automatically execute the standard lifecycle.

This allows every operational workflow to behave consistently while implementing different business logic.

---

# Building a New Workflow

Every new operational workflow should follow the same engineering process.

The objective is to build reusable engineering capabilities rather than isolated automation.

## Step 1 - Understand

Understand the current manual process.

Gather:

- existing documentation
- production procedures
- reference scripts
- operational requirements

Existing production scripts should be treated as reference implementations whenever practical.

---

## Step 2 - Define the Workflow

Identify:

- workflow inputs
- expected outputs
- validation requirements
- execution steps
- verification requirements

Document the workflow before implementation begins.

---

## Step 3 - Implement Workflow Stages

Implement only the workflow-specific stages.

Examples:

- workflow preparation
- validation
- execution
- verification

Common functionality should remain inside the Workflow Engine.

---

## Step 4 - Validate

Run the workflow in planning mode.

Confirm:

- inputs
- validation
- generated plan
- expected actions

No changes should occur during this stage.

---

## Step 5 - Execute

Execute the workflow using validated inputs.

Execution should follow the generated plan whenever practical.

---

## Step 6 - Verify

Confirm that execution produced the desired state.

Verification should become part of every workflow rather than an optional activity.

---

## Step 7 - Generate Documentation

Generate:

- execution report
- validation report
- completion documentation
- request summary

Documentation should be generated whenever practical.

---

## Step 8 - Review

Review the completed workflow.

Questions to consider:

- Can this stage become more reusable?
- Can validation be generalized?
- Can reporting be shared?
- Can documentation be standardized?

Every completed workflow should improve the engineering platform.

---

# Engineering Philosophy

The objective is not to automate individual operational tasks.

The objective is to improve the engineering platform.

Each completed workflow should make future workflows easier to implement, more consistent, and more reliable.


---

# Relationship to the Platform

The Workflow Engine is one component of the overall Power Infrastructure architecture.

```
                    Power Infrastructure

                           │

            ┌──────────────┼──────────────┐
            │              │              │

        Inventory      Workflow Engine    Documentation

            │              │              │

            │        Executes Workflows   │

            │              │              │

            └──────────────┼──────────────┘

                           │

                      Generated Reports

                           │

                    Operational Automation
```

The Workflow Engine consumes validated inventory, executes standardized workflows, and generates operational artifacts that become part of the project's documentation.

It serves as the common execution framework for all operational automation.

---

# Relationship to `pwr`

The `pwr` command-line interface provides the primary interface to the Workflow Engine.

Users should interact with workflows through `pwr` rather than executing playbooks directly.

Examples include:

```
pwr workflow plan

pwr workflow execute

pwr workflow verify

pwr workflow report
```

As the project evolves, additional commands should build upon the same workflow model.

---

# Relationship to Abbey Root

Abbey Root serves as the research and development environment for concepts implemented by the Workflow Engine.

New workflow patterns, command-line features, documentation standards, and engineering practices should be developed and refined in Abbey Root before being adopted into Power Infrastructure.

Both projects should share the same architectural philosophy while serving different purposes.

Abbey Root focuses on experimentation and framework development.

Power Infrastructure focuses on production engineering and operational reliability.

---

# Long-Term Direction

The Workflow Engine is intended to become the standard execution framework for every operational capability developed within Power Infrastructure.

Future workflows—including inventory collection, user administration, backup operations, lifecycle management, patch management, and disaster recovery—should all implement the same workflow contract.

This approach provides a consistent engineering experience, simplifies maintenance, improves documentation, and encourages the development of reusable automation components.

---

# Summary

The Workflow Engine is the foundation of the Power Infrastructure engineering platform.

It separates workflow orchestration from workflow implementation, allowing operational capabilities to be developed independently while maintaining a consistent execution model.

By standardizing the workflow lifecycle, Power Infrastructure can grow without increasing architectural complexity, ensuring that each new capability strengthens the platform rather than creating another standalone solution.
