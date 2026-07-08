# Start Here

Welcome to Power Infrastructure.

If this is your first time working with the project, this document will help you understand what Power Infrastructure is, how the repository is organized, and how to begin an engineering session.

You do **not** need to understand every part of the repository before contributing. The documentation and command-line tools are designed to guide you through the normal engineering workflow.

---

# What is Power Infrastructure?

Power Infrastructure is an engineering platform for managing IBM Power environments.

The project combines automation, reporting, operational workflows, documentation, and infrastructure tooling into a single, reusable platform.

Power Infrastructure is built using the Abbey Framework, applying the same engineering practices, documentation standards, and workflow used by Abbey Root to an enterprise IBM Power environment.

---

# Your First Commands

Most engineering sessions begin with:

```bash
pwr session
```

This command summarizes the current state of the project and reminds you of the standard engineering workflow.

Other useful commands include:

```bash
pwr help
pwr status
pwr doctor
pwr version
```

If you are unsure what to do next, start with `pwr session`.

---

# The Engineering Workflow

Every engineering session follows the same process.

1. Review the current project status.
2. Define one clear objective.
3. Build the change.
4. Validate the results.
5. Update the documentation.
6. Capture what was learned.
7. Commit a logical unit of work.
8. Review the next steps.

Following the same workflow keeps the platform maintainable and ensures knowledge is preserved over time.

---

# Where to Find Information

| Location                | Purpose                                                           |
| ----------------------- | ----------------------------------------------------------------- |
| `docs/guide/`           | Getting started and daily usage.                                  |
| `docs/planning/`        | Project status, roadmap, backlog, and priorities.                 |
| `docs/architecture/`    | Power Infrastructure architecture and technical design.           |
| `docs/framework/`       | Abbey Framework standards adopted by this project.                |
| `docs/reference/`       | IBM Power, HMC, Pure Storage, and environment reference material. |
| `docs/runbooks/`        | Operational procedures and repeatable tasks.                      |
| `docs/generated/`       | Automatically generated documentation and reports.                |
| `docs/session-updates/` | Summaries of completed engineering sessions.                      |

---

# The Philosophy

Power Infrastructure is more than a collection of automation scripts.

The goal is to build a maintainable engineering platform where operational knowledge, documentation, automation, and reporting evolve together.

Whenever practical, improvements should become reusable capabilities rather than one-off solutions.

---

# Where to Go Next

After reading this document:

1. Run `pwr session`.
2. Review `docs/planning/PROJECT_STATUS.md`.
3. Review `docs/planning/NEXT.md`.
4. Define one objective for the session.
5. Begin building.

Welcome to Power Infrastructure.

