# Power Infrastructure CLI Reference

*Generated automatically from `config/cli/cli.yml`. Do not edit directly.*

## Overview

Power Infrastructure Toolkit

```text
pwr <command> [options]
```

## Core CLI

### `pwr doctor`

Run repository and environment health checks.

**Usage**

```text
pwr doctor
```

**Examples**

```text
pwr doctor
```

### `pwr help`

Show Power Infrastructure CLI help.

**Usage**

```text
pwr help
```

**Examples**

```text
pwr help
```

### `pwr version`

Show project version and information.

**Usage**

```text
pwr version
```

**Examples**

```text
pwr version
```

## Git and repository

### `pwr commit-check`

Run validation and show Git status before commit.

**Usage**

```text
pwr commit-check
```

**Examples**

```text
pwr commit-check
```

### `pwr status`

Show local repository status.

**Usage**

```text
pwr status
```

**Examples**

```text
pwr status
```

## Build and validation

### `pwr build`

Run project build checks and regenerate generated documentation.

**Usage**

```text
pwr build
```

**Examples**

```text
pwr build
```

### `pwr validate`

Validate project structure and required files.

**Usage**

```text
pwr validate
```

**Examples**

```text
pwr validate
```

## Documentation

### `pwr docs`

View and generate project documentation.

**Usage**

```text
pwr docs <command>
```

**Subcommands**

- `cli` - Generate CLI reference documentation.
  - `pwr docs cli`
- `generated` - List generated inventory, documentation, and reports.
  - `pwr docs generated`
- `sources` - List source inventory files.
  - `pwr docs sources`
- `summary` - View generated environment summary.
  - `pwr docs summary`

**Examples**

```text
pwr docs cli
pwr docs generated
```

### `pwr publish`

Publish generated documentation.

**Usage**

```text
pwr publish docs
```

**Subcommands**

- `docs` - Publish generated documentation.
  - `pwr publish docs`

**Examples**

```text
pwr publish docs
```

## Reporting

### `pwr report`

Run reporting workflows.

**Usage**

```text
pwr report <command>
```

**Subcommands**

- `monthly-cpu` - Generate monthly HMC CPU capacity report.
  - `pwr report monthly-cpu --collection-date YYYY-MM-DD --period YYYYMM --collector HMC`
- `service-review` - Prepare Service Review reporting package.
  - `pwr report service-review`

**Examples**

```text
pwr report monthly-cpu --collection-date 2026-07-01 --period 202607 --collector txhmcp04
pwr report service-review
```

### `pwr service-review`

Prepare monthly Service Review workflow.

**Usage**

```text
pwr service-review
```

**Examples**

```text
pwr service-review
```

## Request lifecycle

### `pwr request`

Create and manage request workspaces.

**Usage**

```text
pwr request <command|request_id>
```

**Aliases**

- `pwr req`

**Subcommands**

- `archive` - Archive a completed request.
  - `pwr request archive <request_id>`
- `completed` - Mark a request completed.
  - `pwr request completed <request_id>`
- `create` - Create a new request workspace.
  - `pwr request create <request_id>`
- `open` - Open an existing request workspace.
  - `pwr request open <request_id>`

**Examples**

```text
pwr request REQ0722461
pwr request open REQ0722461
pwr request completed REQ0722461
```

## Automation and playbook

### `pwr playbook`

Discover, inspect, search, and run available playbooks.

**Usage**

```text
pwr playbook <command|playbook>
```

**Aliases**

- `pwr pb`

**Subcommands**

- `list` - List available playbooks.
  - `pwr playbook list`
- `search` - Search available playbooks.
  - `pwr playbook search <term>`
- `show` - Show playbook details.
  - `pwr playbook show <playbook>`

**Examples**

```text
pwr playbook
pwr playbook show users/add_user.yml
pwr playbook search user
pwr playbook add-user --check
```

## Workflow

### `pwr workflow`

Run Workflow Engine commands.

**Usage**

```text
pwr workflow <command>
```

**Examples**

```text
pwr workflow help
pwr workflow prepare
```

