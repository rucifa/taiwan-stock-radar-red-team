# SECURITY_SCOPE

This repository is a sanitized public audit mirror.

## Included

- current core specifications
- sanitized scheduler summary
- sample daily JSON/report/state files
- selected Raw + metadata for five trading dates
- one TPEx same-day revision replay case
- a compact 50-entry Raw evidence manifest

## Excluded

- production Git history and personal commit metadata
- Actions logs/artifacts
- credentials, secrets and tokens
- automation task identifiers and unrelated runtime identifiers
- the full legacy Raw/archive/evidence corpus

Files under `raw_evidence/` are intentionally published for independent audit. Public metadata keeps replay-critical date/hash/time/size fields while unrelated runtime identifiers may be omitted.
