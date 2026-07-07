---

date: 2026-07-07
title: CLI Metadata Framework and Playbook Discovery
status: completed
-----------------

# Session Update

## Summary

Focused on completing several small backlog items without introducing new architectural complexity. The work naturally evolved into establishing a metadata-driven framework for the `pwr` command-line interface.

A new `config/cli/cli.yml` file was introduced as the single source of truth for CLI commands, categories, descriptions, aliases, examples, and subcommands. A reusable Python utility (`scripts/power_cli.py`) now consumes this metadata to generate both interactive help output and a Markdown CLI reference.

The playbook subsystem was also expanded with inspection and search capabilities, making available automation easier to discover and understand.

Overall, the session shifted the CLI from a collection of individual command scripts toward a reusable framework that can be extended over time and aligned with Abbey Root.

## Completed

### CLI Metadata Framework

* Created `config/cli/cli.yml` as the authoritative CLI metadata source.
* Added command categories.
* Added subcommand definitions.
* Added aliases.
* Added support for hidden commands.
* Added command examples.

### CLI Framework

* Created reusable `scripts/power_cli.py`.
* Generated `pwr help` output from CLI metadata.
* Generated `docs/generated/CLI_REFERENCE.md` from CLI metadata.
* Added alias support to generated help and documentation.
* Added common task examples to CLI help.

### Playbook Commands

* Added `pwr playbook show`.
* Added `pwr playbook search`.
* Added support for playbook lookup by:

  * friendly name
  * relative path
  * filename
  * full playbook path

### Documentation

* Added `pwr docs cli`.
* Integrated CLI reference generation into the documentation framework.
* Updated `pwr build` to regenerate CLI documentation automatically.

### Project Health

* Updated `pwr doctor` to validate the presence of CLI metadata.

## Architectural Progress

Today's work established a reusable CLI framework:

```text
config/cli/cli.yml
            │
            ▼
     scripts/power_cli.py
      ├── pwr help
      ├── pwr docs cli
      └── CLI_REFERENCE.md
```

This establishes a true single source of truth for the CLI and lays the foundation for future capabilities such as:

* auto-generated help
* shell completion
* command search
* router validation
* CLI documentation
* command metadata validation

## Backlog Items Completed

### Power CLI

* Command metadata standard
* `pwr playbook show`
* Search playbooks
* Auto-generated `pwr help`
* Auto-generated Markdown CLI reference
* Common task examples in help output

### Documentation

* Expanded generated documentation through automatic CLI reference generation.

## Lessons Learned

* Small improvements can uncover reusable architectural patterns.
* Metadata-driven generation significantly reduces duplicated CLI documentation.
* Generating documentation during `pwr build` aligns with the project's "documentation should be generated" philosophy.
* A reusable metadata engine is preferable to embedding formatting logic inside multiple command scripts.

## Next Steps

* Compare `abbey` and `pwr` command structures for consistency.
* Continue standardizing CLI terminology between the two projects.
* Evaluate moving CLI metadata handling into a reusable library under `tools/lib`.
* Expand metadata consumers to support shell completion, router validation, and command-specific help.

