# Using the Power Infrastructure CLI

## Purpose

The Power Infrastructure command-line interface (`pwr`) is the primary way to interact with the project.

Rather than remembering individual scripts, reports, and operational tools, the CLI provides a consistent interface for common engineering tasks.

Think of the CLI as the front door to the platform.

---

# The Philosophy

The CLI exists to make engineering work predictable and discoverable.

Instead of asking:

> "Where is the script that does this?"

the goal is to ask:

> "What am I trying to accomplish?"

As Power Infrastructure evolves, new capabilities should be added through the CLI so the user experience remains consistent.

---

# Discovering Commands

If you're unsure what commands are available, start with:

```bash
pwr help
```

Useful everyday commands include:

```bash
pwr status
pwr doctor
pwr version
pwr session
```

---

# Starting an Engineering Session

Every engineering session should begin with:

```bash
pwr session
```

This command provides:

* Current repository status
* Planning reminders
* Engineering workflow
* Suggested next steps

If you only remember one command, remember `pwr session`.

---

# Universal Commands

Power Infrastructure follows the Abbey Framework.

The following commands have the same meaning across all Abbey-style projects.

| Command    | Purpose                                     |
| ---------- | ------------------------------------------- |
| `help`     | Discover available commands.                |
| `version`  | Identify the project and framework version. |
| `status`   | Show the current project state.             |
| `doctor`   | Validate the project and environment.       |
| `session`  | Begin a structured engineering session.     |
| `build`    | Generate project artifacts.                 |
| `validate` | Verify project consistency.                 |
| `publish`  | Publish project outputs.                    |

---

# Power Infrastructure Commands

Power Infrastructure extends the framework with commands specific to IBM Power engineering.

Examples include:

* `request`
* `playbook`
* `report`
* `service-review`
* `workflow`

These commands build on the framework while preserving the behavior of the universal commands.

---

# Command Discovery

The CLI is metadata-driven.

Command descriptions, examples, categories, and generated documentation are produced from a single source of truth.

This keeps help output and documentation synchronized as the platform evolves.

---

# Daily Workflow

A typical engineering session looks like:

```text
pwr session
      ↓
pwr status
      ↓
Engineering work
      ↓
pwr build
      ↓
pwr validate
      ↓
Documentation
      ↓
Commit
```

---

# The Goal

The CLI is more than a launcher for scripts.

It provides a consistent engineering interface that allows automation, documentation, reporting, and operational workflows to evolve together while remaining familiar to anyone who has used an Abbey-style project.

