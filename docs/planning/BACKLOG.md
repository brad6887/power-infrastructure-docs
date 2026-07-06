# Power Infrastructure Backlog

## High Priority

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

#### Workflow Improvements

- [ ] Generic workflow reporting
- [ ] Standard execution result object
- [ ] Markdown execution reports
- [ ] Capture operator, execution time, validation results, and execution results
- [ ] Store generated artifacts inside the request workspace
- [ ] Minimize prepared user objects by workflow

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

### Power CLI

- [x] Repository-aware playbook execution
- [x] Automatic playbook discovery
- [x] `pwr request`

- [ ] Nested commands
- [ ] `pwr user`
- [ ] `pwr backup`
- [ ] `pwr restore`
- [ ] `pwr docs`
- [ ] `pwr report`
- [ ] `pwr playbook show`
- [ ] Search playbooks
- [ ] Execution history
- [ ] Colorized output
- [ ] Shell completion

---

### Reporting Framework

- [ ] Standard report role
- [ ] Markdown reports
- [ ] HTML reports
- [ ] PDF reports
- [ ] Workflow summaries
- [ ] Execution summaries

---

### Documentation Engine

- [ ] Request documentation
- [ ] Execution documentation
- [ ] Environment documentation
- [ ] Inventory documentation
- [ ] HMC documentation
- [ ] VIOS documentation
- [ ] LPAR documentation
- [ ] Disaster Recovery documentation
- [ ] Capacity documentation

---

## Medium Priority

### Backup Operations

- [ ] Backup validation
- [ ] Restore automation
- [ ] Restore validation
- [ ] Restore reporting
- [ ] Fleet operational summaries

---

### LPAR Lifecycle

- [ ] Deployment
- [ ] Decommissioning
- [ ] Validation
- [ ] Documentation

---

### Inventory

- [ ] Metadata merge
- [ ] Override file
- [ ] Maintenance groups
- [ ] Environment metadata

---

### Common Framework

- [ ] Enterprise defaults
- [ ] Request parser
- [ ] Communications role
- [ ] Documentation role
- [ ] Reporting role
- [ ] Standard result object

---

## Long Term

### Disaster Recovery

- [ ] Documentation generation
- [ ] Recovery planning
- [ ] Deployment automation
- [ ] Validation

### Patch Management

- [ ] Alternate disk validation
- [ ] Alternate disk deployment
- [ ] Rollback planning
- [ ] Reporting

### Platform Upgrades

- [ ] AIX 7.3
- [ ] VIOS

### Enterprise Reporting

- [ ] Operational dashboards
- [ ] Capacity reporting
- [ ] Compliance reporting
- [ ] Change reporting

---

## Future Ideas

### Work Management

- [ ] Incident workspaces
- [ ] Change workspaces
- [ ] Maintenance workspaces
- [ ] Request archive
- [ ] Timeline tracking

### Developer Experience

- [ ] Role generator
- [ ] Workflow generator
- [ ] Project templates
- [ ] Installer improvements
- [ ] Fresh clone validation

### Website Integration

- [ ] Publish generated documentation
- [ ] Status dashboard
- [ ] Operational reports
- [ ] Documentation portal
