# Taiwan Stock Radar — Public Red-Team Mirror

This repository is a **sanitized public audit mirror**, not the production database.

## Purpose

Allow independent Red Team reviewers to evaluate the current simplified daily architecture and a selected five-trading-day Raw evidence pack without exposing production Git history, Actions logs/artifacts, credentials, private automation identifiers, or unrelated legacy evidence.

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
4. `RAW_DATA_RED_TEAM_REQUEST.md`
5. `raw_evidence/README.md`
6. `raw_evidence/RAW_EVIDENCE_MANIFEST.json`
7. `raw_evidence/2026-09-29/` through `raw_evidence/2026-10-05/`
8. `raw_evidence/revision_cases/`
9. `sample/data/2026/2026-10-05.json`, report and latest-state sample

## Evidence boundary

The public Raw pack contains selected evidence for five Taiwan trading dates: 2026-09-29, 2026-09-30, 2026-10-01, 2026-10-02 and 2026-10-05. It is intended for data-integrity, date, provenance, hash and replay review.

Long-term 00:00 / 07:00 unattended scheduler reliability is a separate runtime observation and is not a prerequisite for judging whether the rules and five-day evidence are sufficient to proceed.

## Explicit exclusions

This mirror intentionally excludes:

- production Git history and personal commit metadata
- GitHub Actions logs/artifacts
- secrets / credentials
- private repository location
- ChatGPT automation task IDs and unrelated scheduler/run identifiers
- the full Legacy A2 raw/archive/evidence corpus
- internal historical regression packs not required for this audit

The selected five-day Raw evidence under `raw_evidence/` is intentionally included and sanitized for public Red Team review.
