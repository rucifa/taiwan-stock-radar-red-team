# Five-Day Raw Evidence Pack

## Purpose

This directory is the minimum public evidence set for an independent Red Team to test whether the current Taiwan Stock Radar data rules are sufficiently correct, traceable and replayable to proceed.

Trading dates:

- 2026-09-29
- 2026-09-30
- 2026-10-01
- 2026-10-02
- 2026-10-05

This is a **data-integrity / replay / source-contract** evidence pack, not a long-term scheduler-reliability certification.

## Coverage

Each date contains one selected final snapshot for these 10 daily source families:

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

The main manifest contains 50 unique `(trading_date, source_id)` entries.

A separate 2026-09-29 `TPEX_3INSTI_HTML` before/after pair is under `revision_cases/` for same-day revision replay.

## Metadata policy

Raw bytes are preserved. Public metadata is either copied directly or minimally sanitized to remove unrelated runtime/scheduler identifiers. Replay-critical source ID, business key when present, first-seen time, Raw SHA-256, content type and byte size are preserved in the public evidence or main manifest.

For older metadata where `business_key` is null, reviewers must not invent a date; use Raw/source semantics and mark any unresolved date assertion explicitly.

## Red-Team checks

Independently test:

1. 5 dates × 10 sources = 50 covered date/source pairs.
2. Every manifest Raw/meta path exists and Raw files are non-empty.
3. Raw SHA-256 matches the manifest/metadata.
4. Claimed business dates are correct and stale prior-day data is not silently accepted.
5. Structured payloads are materially parseable and schema drift cannot false-PASS.
6. Missing/not-published/stale/error values cannot silently become zero.
7. The 2026-09-29 revision pair preserves two distinct versions and can be replayed without overwrite.
8. Any defect that materially affects data correctness, traceability, replay or analysis safety is identified with a reproducible path.

## Decision rule

- `PASS` — proceed.
- `PASS_WITH_FOLLOW_UP` — proceed; non-blocking items become backlog.
- `CORRECTIVE_REQUIRED` — only for a demonstrated material defect.
- `INSUFFICIENT_EVIDENCE` — identify the exact missing evidence; do not redesign unrelated governance.

Long-term 00:00 / 07:00 unattended scheduler reliability is a **separate runtime observation**, not a blocker for this five-day data/rule Red Team decision.
