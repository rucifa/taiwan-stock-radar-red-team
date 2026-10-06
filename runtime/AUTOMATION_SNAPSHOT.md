# AUTOMATION_SNAPSHOT

**Snapshot date:** 2026-10-06  
**Timezone:** Asia/Taipei

## Active production tasks

### 1. Daily Taiwan Market Radar — Fetch + Store + Analyze

- Enabled: YES
- Schedule: Tue–Sat 00:00 Asia/Taipei
- First simplified-flow schedule: 2026-10-07 00:00
- Responsibilities:
  1. Resolve target trading day.
  2. Fetch official market data, with reliable supplemental sources only when necessary.
  3. Normalize and save daily data.
  4. Read required historical data and calculate derived metrics.
  5. Produce the full daily market radar in the same execution.
  6. Save the daily report.
  7. Update `state/latest.json`.
  8. Produce a user-visible result.
- Partial records are allowed and required when the target is a confirmed trading day but some sources are missing.
- Legacy A2 / Gate A / Recovery contamination is not a production gate.

### 2. Daily Taiwan Data Verification — Verify + Repair

- Enabled: YES
- Schedule: Tue–Sat 07:00 Asia/Taipei
- First simplified-flow schedule: 2026-10-07 07:00
- Responsibilities:
  1. Read the existing target-date daily record and report.
  2. Verify business date, source provenance, publication delays, stale/error states and official revisions.
  3. Re-fetch and repair affected fields when necessary.
  4. Recalculate affected derived metrics.
  5. Update `state/latest.json`.
  6. Rebuild the full market radar only if the repair materially changes regime, radar score, opportunity level, new-investment decision, extra-pool percentage, All-in suitability, key risk interpretation, or materially relevant data confidence.

## Disabled legacy tasks

Legacy Operational Trigger / Recovery and Formal Recovery tasks are disabled and are not part of the current production topology.

## Red-Team boundary

Review the architecture above as the current production scheduler contract. Do not reopen Legacy A2 as a required daily gate unless a concrete current-flow defect requires it.
