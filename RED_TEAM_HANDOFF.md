# Red-Team Handoff

## Goal

Decide whether the current Taiwan Stock Radar rules and existing five-day real-market evidence are sufficiently sound to proceed to the next phase.

## Read order

1. `core/README_FIRST.md`
2. `core/DAILY_MARKET_RADAR_SPEC.md`
3. `core/MARKET_RADAR_ANALYSIS_SPEC.md`
4. `RED_TEAM_AUDIT_REQUEST.md`
5. `RAW_DATA_RED_TEAM_REQUEST.md`
6. `raw_evidence/README.md`
7. `raw_evidence/RAW_EVIDENCE_MANIFEST.json`
8. Five dated directories under `raw_evidence/`
9. `raw_evidence/revision_cases/`
10. Existing `sample/` simplified daily record/report for contract review

## Decision boundary

The Red Team is being asked whether the **rules + existing real data evidence** are adequate to move forward.

The future accumulation of 00:00 / 07:00 scheduled runtime evidence is separate operational monitoring. Lack of long-term runtime statistics by itself is not a blocker.

## Stop rule

If verdict is `PASS` or `PASS_WITH_FOLLOW_UP`, proceed to the next phase.

If `CORRECTIVE_REQUIRED`, correct only demonstrated blocking defects and run a bounded targeted retest.

If `INSUFFICIENT_EVIDENCE`, request the exact missing evidence only.

No new evidence → no new validation iteration.
