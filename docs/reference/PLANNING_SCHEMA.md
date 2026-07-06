# Planning Schema

This document defines the purpose of each planning document used throughout the Power Infrastructure project.

Each planning document has a single responsibility.

Avoid duplicating information across planning documents.

---

# PROJECT_STATUS.md

Purpose:

Describe the current state of the project.

Contents may include:

- Current focus
- Recent accomplishments
- Active development
- Current architecture
- Overall project health

This document answers:

> "Where does the project stand today?"

---

# NEXT.md

Purpose:

Describe the next engineering tasks.

Contents should include:

- Immediate priorities
- Next work session goals
- Short-term tasks
- Work currently in progress

This document answers:

> "What should I work on next?"

---

# BACKLOG.md

Purpose:

Maintain a prioritized list of future work.

Contents include:

- Features
- Enhancements
- Technical debt
- Ideas ready for implementation

Backlog items are not necessarily scheduled.

This document answers:

> "What work remains?"

---

# ROADMAP.md

Purpose:

Describe the long-term direction of the project.

Roadmaps should describe capabilities rather than individual tasks.

Examples include:

- Disaster recovery
- Lifecycle management
- Inventory platform
- Documentation generation
- Workflow engine

This document answers:

> "Where is the project heading?"

---

# MILESTONES.md

Purpose:

Track major project achievements.

Milestones represent significant engineering accomplishments.

Examples:

- Inventory complete
- Workflow engine implemented
- User administration complete
- Disaster recovery operational

This document answers:

> "What major objectives have been achieved?"

---

# VISION.md

Purpose:

Describe the long-term vision for the project.

Unlike the roadmap, the vision should remain relatively stable over time.

It explains:

- why the project exists
- what success looks like
- long-term engineering philosophy

This document answers:

> "What are we ultimately trying to build?"

---

# IDEAS.md

Purpose:

Capture ideas before they become planned work.

Ideas may include:

- architectural concepts
- automation opportunities
- research topics
- future enhancements

Ideas should be reviewed periodically.

Promising ideas may move into the backlog.

This document answers:

> "What possibilities should we explore?"

---

# Relationship Between Planning Documents

```
Vision
    │
    ▼
Roadmap
    │
    ▼
Backlog
    │
    ▼
Next
    │
    ▼
Project Status
```

Ideas may enter the planning process at any point and are evaluated before becoming backlog items.

---

# Review Frequency

Each document should be reviewed at different intervals.

| Document | Typical Review |
|----------|----------------|
| Project Status | Every session |
| Next | Every session |
| Backlog | Weekly |
| Roadmap | Monthly |
| Milestones | After major accomplishments |
| Vision | Occasionally |
| Ideas | Whenever inspiration occurs |

---

# Planning Philosophy

Planning documents should evolve naturally.

Avoid maintaining duplicate information.

Each document should answer one specific question and work together with the others to provide a complete picture of the project's direction and progress.
