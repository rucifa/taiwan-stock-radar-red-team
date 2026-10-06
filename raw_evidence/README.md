# Five-Day Raw Evidence Pack

## Purpose

This directory is the minimum public evidence set for an independent Red Team to test whether the current Taiwan Stock Radar data rules are sufficiently correct and traceable to proceed to the next project phase.

The five consecutive Taiwan trading dates are:

- 2026-09-29
- 2026-09-30
- 2026-10-01
- 2026-10-02
- 2026-10-05

This is a **data-integrity / replay / source-contract** evidence pack. It is not a long-term scheduler-reliability certification.

## Included source families

For each of the five dates, the pack includes one preserved final snapshot plus its original metadata for:

- TWSE_DAILY_ALL_CSV
- TPEX_DAILY_CLOSE_CSV
- TWSE_T86_HTML
- TPEX_3INSTI_HTML
- TWSE_MARGIN_HTML
- TPEX_MARGIN_HTML
- TWSE_SHORT_LENDING_HTML
- TPEX_SHORT_LENDING_HTML
- TWSE_CORPORATE_ACTION_CSV
- TPEX_CORPORATE_ACTION_CSV

A separate preserved 2026-09-29 TPEx 3-institutional before/after revision pair is also included for revision replay.

## Directory shape

```text
raw_evidence/
├─ README.md
├─ RAW_EVIDENCE_MANIFEST.json
├─ 2026-09-29/
├─ 2026-09-30/
├─ 2026-10-01/
├─ 2026-10-02/
├─ 2026-10-05/
└─ revision_cases/
```

Every copied Raw file is accompanied by its original `.meta.json`. The manifest records the public path and the key provenance fields used for audit.

## What the Red Team should prove

The Red Team should independently test:

1. Raw content belongs to the claimed business date where a business date is applicable.
2. No prior-day/stale payload is silently accepted as the target date.
3. Raw SHA-256 and semantic provenance are coherent with metadata.
4. Structured payloads are non-empty and materially parseable.
5. Cross-source date coverage is coherent across the five-day window.
6. The 2026-09-29 revision pair can be distinguished and replayed without overwrite.
7. Metadata is sufficient to trace Raw → source → business date → first-seen/revision semantics.
8. Any concrete defect that would make the simplified daily data rules unsafe is identified.

## Decision rule

The purpose is to decide whether the project can proceed, not to create another open-ended governance loop.

Allowed overall verdicts:

- `PASS` — proceed.
- `PASS_WITH_FOLLOW_UP` — proceed; non-blocking items become follow-up backlog.
- `CORRECTIVE_REQUIRED` — only for a demonstrated defect that materially affects data correctness, traceability, replay, or analysis safety.
- `INSUFFICIENT_EVIDENCE` — identify the exact missing evidence; do not redesign unrelated governance.

## Scheduler separation

The 00:00 Fetch + Store + Analyze and 07:00 Verify + Repair schedules continue to accumulate real runtime evidence naturally.

Long-term unattended scheduling reliability is a **separate runtime observation** and is **not a prerequisite for the Red Team to decide whether the current rules and five-day data evidence are sufficient to proceed**.

## Excluded from this public pack

- private production repository identity
- private Git history
- personal commit metadata
- GitHub Actions logs/artifacts
- automation task IDs
- full Legacy A2 manifests/evidence corpus
- monthly-revenue source (not a daily market source for this five-day test window)
