# HMC Scan Flow

## Purpose

Document the future process for moving HMC scan reports from `txapnim01` to `txvadmp25`.

## Current State

- HMC Scanner runs on `txapnim01`.
- Power Infrastructure runs on `txvadmp25`.
- Importing is currently manual.
- Transfer automation still needs to be designed.

## Target Flow

```text
txapnim01
  run HMC scan
  archive .xls files
  copy latest .xls files to txvadmp25

txvadmp25
  receive files in inventory/source/
  import HMC report
  generate inventory.json
  generate docs/reports
