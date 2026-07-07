# Power Infrastructure Backlog

## High Priority

### Workflow Framework

- [ ] Generic workflow reporting
- [ ] Standard execution result object
- [ ] Standard workflow metadata
- [ ] Markdown execution reports
- [ ] Capture operator, execution time, validation results, and execution results
- [ ] Store generated artifacts inside the request workspace
- [ ] Minimize prepared user objects by workflow

---

### Power CLI

- [x] Repository-aware playbook execution
- [x] Automatic playbook discovery
- [x] `pwr request`
- [x] `pwr playbook show`
- [x] Search playbooks
- [x] Command metadata standard
- [x] Auto-generated `pwr help`
- [x] Auto-generated Markdown CLI reference
- [x] Common task examples in help output

- [ ] Nested commands
- [ ] `pwr user`
- [ ] `pwr backup`
- [ ] `pwr restore`
- [x] `pwr docs`
- [ ] `pwr report`
- [ ] Execution history
- [ ] Colorized output
- [ ] Shell completion
- [ ] Keep `pwr` and `abbey` command documentation aligned
- [ ] Command metadata validation
- [ ] Auto-generated shell completion
- [ ] Command-specific help (`pwr <command> help`)
- [ ] Router generation/validation from CLI metadata

---

### Service Review

- [x] HMC performance import
- [x] HMC normalization
- [x] CPU capacity reporting
- [x] Pure CLI collection
- [x] Pure normalization
- [x] Pure capacity widget
- [x] Service Review preparation command

Remaining

- [ ] Pure1 API collector
- [ ] Replication lag reporting
- [ ] HMC automatic collection
- [ ] Pure automatic API collection
- [ ] Service Review playbook
- [ ] PowerPoint generation
- [ ] Email delivery

---

### Request Lifecycle

- [x] `pwr request`
- [ ] Request metadata (`request.yml`)
- [ ] Request status tracking
- [ ] Open / In Progress / Completed / Archived
- [ ] Completion timestamps
- [ ] Request owner
- [ ] Workflow type
- [ ] `pwr request open`
- [ ] `pwr request completed`
- [ ] `pwr request archive`
- [ ] Request statistics
- [ ] Request summaries

---

### Documentation Framework

- [ ] Review planning documents
- [ ] Review guide documents
- [ ] Review reference documents
- [ ] Standardize documentation with Abbey Root
- [x] Expand generated documentation
- [ ] Documentation quality validation

---

### Reporting Framework

- [ ] Standard report role
- [ ] Markdown reports
- [ ] HTML reports
- [ ] PDF reports
- [ ] Workflow summaries
- [ ] Execution summaries

### Reporting Framework

- [ ] Generic report data model
- [ ] Markdown renderer
- [ ] CSV renderer
- [ ] HTML renderer
- [ ] JSON renderer
- [ ] PDF renderer
- [ ] Email delivery
- [ ] Documentation publishing

---

### User Administration

#### Complete User Lifecycle

- [ ] Make user creation fully idempotent
- [ ] Complete user removal workflow
- [ ] Create `aix_user_validate_remove`
- [ ] User lock
- [ ] User unlock
- [ ] Password reset
- [ ] Standalone SSH key management
- [ ] Multiple SSH key support

---

## Medium Priority

### CLI Framework

- [ ] Move CLI metadata engine into reusable library
- [ ] Metadata-driven command routing
- [ ] Metadata-driven help for subcommands
- [ ] Metadata validation during build
- [ ] Shared CLI framework with Abbey Root

---

### Backup Operations

- [ ] Backup validation
- [ ] Restore automation
- [ ] Restore validation
- [ ] Restore reporting
- [ ] Fleet operational summaries

---

### Inventory

- [ ] Metadata merge
- [ ] Override file
- [ ] Maintenance groups
- [ ] Environment metadata
- [ ] Historical inventory

---

### Common Framework

- [ ] Enterprise defaults
- [ ] Request parser
- [ ] Communications role
- [ ] Documentation role
- [ ] Reporting role
- [ ] Standard result object

---

### LPAR Lifecycle

- [ ] Deployment
- [ ] Decommissioning
- [ ] Validation
- [ ] Documentation

---

## Low Priority

### Disaster Recovery

- [ ] Documentation generation
- [ ] Recovery planning
- [ ] Deployment automation
- [ ] Validation

---

### Patch Management

- [ ] Alternate disk validation
- [ ] Alternate disk deployment
- [ ] Rollback planning
- [ ] Reporting

---

### Platform Upgrades

- [ ] AIX 7.3 automation
- [ ] VIOS automation

---

### Enterprise Reporting

- [ ] Operational dashboards
- [ ] Capacity reporting
- [ ] Compliance reporting
- [ ] Change reporting
