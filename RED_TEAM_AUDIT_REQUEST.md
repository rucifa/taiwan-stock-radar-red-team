# Independent Red-Team Audit Request

Perform a **read-only independent architecture and data-contract audit** of this repository.

## Authority order

1. `core/README_FIRST.md`
2. `core/DAILY_MARKET_RADAR_SPEC.md`
3. `core/MARKET_RADAR_ANALYSIS_SPEC.md`
4. `core/LEGACY_MIGRATION_NOTE.md`

Do not treat historical Legacy A2 architecture as a current production gate.

## Audit questions

Evaluate whether the current simplified architecture is internally consistent and fail-safe for its intended purpose:

1. Does the 00:00 `Fetch + Store + Analyze` flow form a coherent single-cycle pipeline?
2. Is the 07:00 `Verify + Repair` role clearly separated from the primary 00:00 flow?
3. Are storage paths and `state/latest.json` semantics coherent?
4. Does the system correctly preserve partial records rather than fabricating missing data?
5. Is per-source provenance sufficient (`source_id`, `source_type`, `business_date`, `as_of`, `status`)?
6. Are Missing / Not Published / Stale / Error / N/A states handled without using prior-day data as the target day?
7. Is the boundary between current production flow and Legacy A2 clear enough to prevent accidental governance re-entry?
8. Does the sample daily JSON conform materially to the current specification?
9. Does the sample report conform materially to `MARKET_RADAR_ANALYSIS_SPEC.md`?
10. Are international post-close data correctly restricted to next-session context rather than retroactively changing the target Taiwan-session score?
11. Is the long-term investment / extra-investment logic internally consistent and protected from accidental short-term sell signalling?
12. Identify any architecture blocker, data-integrity blocker, traceability defect, or ambiguity that should be corrected before accumulating runtime evidence.

## Runtime limitation

The 2026-10-05 sample is a migration/backfill record. Therefore:

- You MAY audit architecture, schema, provenance, storage, partial-record handling and report-contract compliance now.
- You MUST NOT claim unattended runtime reliability has been proven.
- Runtime reliability should remain `PENDING_RUNTIME_EVIDENCE` until real simplified-flow scheduled cycles exist.

## Required output

Return:

### Overall Verdict

Choose one:

- `PASS`
- `PASS_WITH_FOLLOW_UP`
- `CORRECTIVE_REQUIRED`
- `INSUFFICIENT_EVIDENCE`

### Finding Matrix

For every finding provide:

- ID
- Severity: BLOCKING / IMPORTANT / FOLLOW_UP
- Evidence path
- Exact issue
- Why it matters
- Recommended bounded correction
- Whether correction changes architecture, scheduler, schema, or only documentation

### Separate verdicts

- Scheduler Architecture
- Storage Contract
- Source Provenance
- Partial-Record Behavior
- Analysis Contract
- Legacy Boundary
- Current Sample Compliance
- Runtime Reliability

Do not recommend additional governance complexity unless it fixes a concrete demonstrated failure mode.
