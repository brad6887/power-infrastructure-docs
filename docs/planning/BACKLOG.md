# Power Infrastructure Backlog

## High Priority

### Operational Review Framework

- [x] `pwr review`
- [x] Multi-host Operational Reviews
- [ ] Fleet operational summaries
- [ ] Fleet operational reports
- [ ] Health dashboards
- [ ] Historical health results
- [ ] Health trend analysis
- [ ] Review scoring
- [ ] Review recommendations
- [ ] Automatic review discovery

---

### Operational Reviews

#### AIX

Completed

- [x] Operating System
- [x] Paging Space
- [x] Memory
- [x] CPU
- [x] Network
- [x] Bootlist
- [x] Boot Device validation
- [x] Dump Device validation
- [x] Disk Path validation
- [x] Filesystem Capacity
- [x] errpt severity analysis

Remaining

- [ ] Filesystem growth history
- [ ] SEA health
- [ ] Performance baseline
- [ ] Service inventory
- [ ] Device health
- [ ] HACMP/PowerHA awareness
- [ ] Alternate disk awareness

#### MQ

Completed

- [x] Queue Manager
- [x] Listener status
- [x] Channel status
- [x] Queue review
- [x] FDC review
- [x] MQ error log review
- [x] AIX errpt integration

Remaining

- [ ] Queue depth thresholds
- [ ] Dead-letter queue review
- [ ] Channel history
- [ ] Authority review
- [ ] Queue manager configuration review

#### Pure Storage

Completed

- [x] CLI connectivity
- [x] Controller health
- [x] Capacity health
- [x] Management certificate review
- [x] Array connection health
- [x] Pod health
- [x] Replica link health
- [x] Open alert review

Remaining

- [ ] Volume health
- [ ] Host connectivity
- [ ] Protection Group health
- [ ] ActiveDR policy validation
- [ ] Snapshot health
- [ ] Hardware component health
- [ ] Performance review
- [ ] Capacity growth history
- [ ] REST API collector

#### Future Reviews

- [ ] VIOS
- [ ] HMC
- [ ] Veeam
- [ ] Oracle
- [ ] Linux
- [ ] NIM

---

### Workflow Framework

- [ ] Generic workflow reporting
- [ ] Standard execution result object
- [ ] Standard workflow metadata
- [ ] Shared evidence model
- [ ] Shared health summary role
- [ ] Markdown execution reports
- [ ] Capture operator, execution time, validation results, and execution results
- [ ] Store generated artifacts inside the request workspace
- [ ] Minimize prepared user objects by workflow

---

### Power CLI

Completed

- [x] Repository-aware playbook execution
- [x] Automatic playbook discovery
- [x] `pwr request`
- [x] `pwr playbook show`
- [x] Search playbooks
- [x] Command metadata standard
- [x] Auto-generated `pwr help`
- [x] Auto-generated Markdown CLI reference
- [x] Common task examples in help output
- [x] `pwr docs`
- [x] `pwr review`

Remaining

- [ ] Nested commands
- [ ] `pwr review all`
- [ ] `pwr user`
- [ ] `pwr backup`
- [ ] `pwr restore`
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

Completed

- [x] HMC performance import
- [x] HMC normalization
- [x] CPU capacity reporting
- [x] Pure CLI collection
- [x] Pure normalization
- [x] Pure capacity widget
- [x] Service Review preparation command
- [x] Pure operational review

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

Completed

- [x] `pwr request`

Remaining

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
- [ ] Generic report data model
- [ ] Markdown renderer
- [ ] HTML renderer
- [ ] CSV renderer
- [ ] JSON renderer
- [ ] PDF renderer
- [ ] Workflow summaries
- [ ] Execution summaries
- [ ] Documentation publishing
- [ ] Email delivery

---

### Patch Management

- [ ] Patch Readiness workflow
- [ ] Reuse Operational Review evidence
- [ ] Alternate disk validation
- [ ] bosboot validation
- [ ] Dump device remediation
- [ ] Alternate disk deployment
- [ ] Rollback planning
- [ ] Reporting
- [ ] Post-patch validation

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
- [ ] Infrastructure inventory (Pure Storage, HMC, future enterprise platforms)
- [ ] Maintenance groups
- [ ] Environment metadata
- [ ] Historical inventory
- [ ] Configuration drift detection

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

- [ ] DR pre-flight operational review
- [ ] DR post-activation validation
- [ ] DR repository synchronization
- [ ] Offline operation guidance
- [ ] Documentation generation
- [ ] Recovery planning
- [ ] Deployment automation
- [ ] Validation

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
