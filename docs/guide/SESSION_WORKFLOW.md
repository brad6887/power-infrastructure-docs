# Session Workflow

The Power Infrastructure project follows a repeatable engineering workflow for every development session.

The goal is to make progress consistent, well documented, and easy to resume while ensuring documentation evolves alongside automation.

---

# Before You Begin

Review the current planning documents.

- Project Status
- Next
- Backlog

Identify the highest-priority engineering task for the session.

Whenever possible, complete one logical unit of work rather than making many unrelated changes.

---

# During the Session

Follow the engineering lifecycle.

## 1. Understand

Understand the current manual process before attempting to automate it.

Existing production scripts should be treated as reference implementations and mined for proven logic before being replaced.

## 2. Document

Document the workflow before writing automation.

The objective is to understand the operational process, not simply reproduce commands.

## 3. Validate

Build inventory collection and prerequisite validation before implementing changes.

Automation should identify problems before making modifications.

## 4. Generate

Whenever practical, generate reports or proposed actions before execution.

Generated output allows review before operational changes occur.

## 5. Automate

Implement reusable automation components.

Favor small Ansible roles and reusable utilities over large monolithic scripts.

## 6. Verify

Confirm that automation completed successfully.

Verification should become part of every workflow rather than an optional step.

## 7. Document Results

Update project documentation before ending the session.

Documentation should remain synchronized with the current state of the project.

---

# End of Session

Before finishing work:

- Update Project Status.
- Update Next.
- Update Backlog if priorities changed.
- Update Roadmap when long-term direction changes.
- Create a Session Update.
- Create a journal entry if appropriate.
- Review generated documentation.
- Commit changes to Git.

---

# Session Updates

Each engineering session should produce a lightweight Session Update describing:

- Summary
- Completed work
- Design decisions
- Operational impact

Session Updates provide a historical record of development and can later be reconciled into planning documentation.

---

# Git Workflow

At the end of each completed engineering task:

1. Review changes.
2. Validate generated documentation.
3. Commit related work together.
4. Push to the repository.
5. Verify repository status is clean.

---

# Engineering Philosophy

The objective of each session is not simply to write automation.

Each session should improve one or more of the following:

- Inventory
- Validation
- Documentation
- Reporting
- Automation
- Verification

Small, incremental improvements produce a more reliable engineering platform over time.
