# Five-Day Raw Data Red-Team Request

Perform an independent, read-only audit of `raw_evidence/` together with the current core specifications in `core/`.

## Primary decision question

> Based on the current rules and the five real trading days of preserved evidence, is the Taiwan Stock Radar data pipeline sufficiently correct, traceable, and replayable to proceed to the next project phase?

Do **not** turn long-term 00:00 / 07:00 scheduler reliability into a prerequisite for this verdict. Scheduled runtime reliability is observed separately as future production cycles execute.

## Audit window

- 2026-09-29
- 2026-09-30
- 2026-10-01
- 2026-10-02
- 2026-10-05

## Required tests

1. Verify source coverage by date against `raw_evidence/RAW_EVIDENCE_MANIFEST.json`.
2. Verify business-date correctness from the Raw payload and metadata where applicable.
3. Look specifically for stale prior-day contamination or wrong-date acceptance.
4. Recompute Raw SHA-256 and compare with metadata/manifest.
5. Check semantic hash / source-scope provenance where provided.
6. Confirm structured Raw payloads are materially parseable and not false-success empty/schema-drift payloads.
7. Check duplicate/revision behavior and the preserved 2026-09-29 TPEx revision case.
8. Test whether the evidence can support deterministic reconstruction of the data inputs needed by the simplified daily flow.
9. Compare the data-handling behavior with `core/DAILY_MARKET_RADAR_SPEC.md`.
10. Identify only concrete blockers that would make daily storage or analysis materially unsafe.

## Required verdict

Choose exactly one:

- `PASS`
- `PASS_WITH_FOLLOW_UP`
- `CORRECTIVE_REQUIRED`
- `INSUFFICIENT_EVIDENCE`

`PASS_WITH_FOLLOW_UP` is explicitly a **GO** verdict. Observability improvements, more runtime samples, documentation polish, and long-term scheduler statistics are non-blocking unless tied to a demonstrated data-integrity failure.

## Finding format

For each finding provide:

- ID
- Severity: `BLOCKING` / `IMPORTANT` / `FOLLOW_UP`
- Evidence path
- Exact reproduced observation
- Why it matters
- Minimal bounded correction
- Retest scope

A `BLOCKING` finding must demonstrate a real failure mode affecting data correctness, target-date integrity, provenance, replayability, or analysis safety.

## Separate assessments

Report separately:

- Five-day source coverage
- Business-date integrity
- Raw/hash integrity
- Structured-data parseability
- Revision/replay behavior
- Metadata/provenance traceability
- Simplified daily-rule compatibility
- Runtime scheduler observation: `SEPARATE_NON_BLOCKING` unless an actual scheduler defect corrupts or misdates stored data

Do not recommend new governance gates without a concrete demonstrated failure mode.
