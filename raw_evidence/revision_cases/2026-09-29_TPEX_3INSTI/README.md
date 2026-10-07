# 2026-09-29 TPEX_3INSTI same-day revision evidence

Purpose: preserve a real same-business-date TPEx institutional-flow revision for independent replay.

- Source: `TPEX_3INSTI_HTML`
- Business date: `2026-09-29`
- Before first seen: `2026-09-29T08:53:58.505498+00:00`
- Before SHA-256: `49b254f3d82f229494bc59c9e21ca6c224c5ec0534a74758444aab8f5b245ca6`
- After first seen: `2026-09-29T09:16:54.966910+00:00`
- After SHA-256: `ab8f727e6012ed48afb427e1a253c9ee1086b1a0f5821313798a5638d56031a1`
- Expected row universe: unchanged
- Previously measured row-level changes: 6
- Added security codes: none
- Removed security codes: none

The two Raw files are preserved unchanged. Reviewers should independently recompute hashes and row-level differences rather than trusting the stated result.

The before metadata is preserved under the original `.html.meta.json` name. The after metadata is published as `after_metadata_sanitized.json`; it retains the replay-critical business date, first-seen time, hashes, row count and byte size while omitting unrelated provenance.
