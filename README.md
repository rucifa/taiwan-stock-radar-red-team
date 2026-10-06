# Taiwan Stock Radar — Public Red-Team Mirror

This repository is a **sanitized public audit mirror**, not the production database.

## Purpose

Allow independent Red Team reviewers to evaluate the current simplified daily architecture without exposing the private production repository, its Git history, Actions logs/artifacts, legacy raw archive, task IDs, credentials, or personal commit metadata.

## Current production model

- Asia/Taipei Tue–Sat 00:00: `Fetch + Store + Analyze`
- Asia/Taipei Tue–Sat 07:00: `Verify + Repair`
- No separate 01:00 production radar task.
- Legacy A2 / Gate A material is historical only and must not gate the current daily flow.
- Canonical daily storage:
  - `data/daily/YYYY/YYYY-MM-DD.json`
  - `reports/daily/YYYY/YYYY-MM-DD.md`
  - `state/latest.json`

## Read order

1. `core/README_FIRST.md`
2. `core/DAILY_MARKET_RADAR_SPEC.md`
3. `core/MARKET_RADAR_ANALYSIS_SPEC.md`
4. `core/LEGACY_MIGRATION_NOTE.md`
5. `runtime/AUTOMATION_SNAPSHOT.md`
6. `sample/data/2026/2026-10-05.json`
7. `sample/reports/2026/2026-10-05.md`
8. `sample/state/latest.json`
9. `RED_TEAM_AUDIT_REQUEST.md`

## Important limitation

The included 2026-10-05 sample is a migration/backfill sample. It is useful for architecture, schema, provenance, partial-record and report-contract review, but **it is not proof of unattended long-term runtime reliability**.

The first full unattended simplified production cycle is expected from 2026-10-07 Asia/Taipei onward.

## Explicit exclusions

This mirror intentionally excludes:

- production Git history
- production commit author/committer metadata
- GitHub Actions logs
- GitHub Actions artifacts
- secrets / credentials
- private repository URL
- ChatGPT automation task IDs
- Legacy A2 raw/archive/evidence corpus
- internal historical regression packs not required for the simplified daily architecture audit
