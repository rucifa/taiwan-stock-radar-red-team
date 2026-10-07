# SOURCE_MANIFEST

Public mirror type: sanitized audit snapshot  
Public evidence scope: current core specs + one normalized/report sample + selected five-trading-day Raw evidence

## Files

| Public mirror path | Source class | Notes |
|---|---|---|
| `core/README_FIRST.md` | Project canonical | public audit copy |
| `core/DAILY_MARKET_RADAR_SPEC.md` | Project canonical | public audit copy |
| `core/MARKET_RADAR_ANALYSIS_SPEC.md` | Project canonical | public audit copy |
| `core/LEGACY_MIGRATION_NOTE.md` | Historical-boundary reference | Legacy A2 does not gate the simplified daily flow |
| `runtime/AUTOMATION_SNAPSHOT.md` | Sanitized scheduler snapshot | private task identifiers omitted |
| `raw_evidence/2026-09-29/` ... `2026-10-05/` | Selected Raw evidence | 10 daily source families × 5 trading dates |
| `raw_evidence/RAW_EVIDENCE_MANIFEST.json` | Replay index | 50 unique date/source entries |
| `raw_evidence/revision_cases/2026-09-29_TPEX_3INSTI/` | Revision evidence | preserved same-day before/after Raw pair |
| `sample/data/2026/2026-10-05.json` | Production daily sample | migration/backfill sample |
| `sample/reports/2026/2026-10-05.md` | Production report sample | migration/backfill sample |
| `sample/state/latest.json` | Production state sample | points to 2026-10-05 |

The mirror intentionally does not expose the production repository location, production commit history, Actions logs/artifacts, credentials, automation task IDs, or the full legacy Raw archive.
