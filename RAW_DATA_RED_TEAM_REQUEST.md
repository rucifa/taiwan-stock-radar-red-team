# 五個交易日資料｜對外紅隊測試提示詞

> **僅在 Public Red-Team GitHub 的五日包已完整寫入且通過基本完整性核對後才使用本提示詞。** 這是給外部 Gemini / Grok / Perplexity 的獨立審查任務，不是要求紅隊修改 GitHub。

請作為獨立 Red Team，**唯讀查核**以下 Public Repository：

**https://github.com/rucifa/taiwan-stock-radar-red-team**

本次只有一個主要決策問題：

> **基於現在的核心規則，以及五個交易日真實 Raw／metadata／hash／修訂 evidence，是否足以證明每日資料流程的正確性、可追溯性與可重播性，並讓「台股投資雷達」專案進入下一階段？**

## 請閱讀

1. `core/README_FIRST.md`
2. `core/DAILY_MARKET_RADAR_SPEC.md`
3. `core/MARKET_RADAR_ANALYSIS_SPEC.md`
4. `RAW_DATA_RED_TEAM_REQUEST.md`
5. `raw_evidence/README.md`
6. `raw_evidence/RAW_EVIDENCE_MANIFEST.json`
7. `raw_evidence/2026-09-29/`
8. `raw_evidence/2026-09-30/`
9. `raw_evidence/2026-10-01/`
10. `raw_evidence/2026-10-02/`
11. `raw_evidence/2026-10-05/`
12. `raw_evidence/revision_cases/`
13. `sample/data/2026/2026-10-05.json`、`sample/reports/2026/2026-10-05.md`、`sample/state/latest.json`

## 必須獨立驗證

- 5 個交易日、每日十種指定來源的 coverage 和 metadata 指標（50 組）。
- Raw bytes 與 SHA-256 是否一致；如無法下載或算 hash，明確列「未驗證」，不能假裝 PASS。
- 真實 Raw 日期與 `business_key` 是否正確，是否會把先前交易日的 stale data 誤認為 target date。
- 原始檔是否非空、可解析、沒有 schema drift 或 false PASS。
- 缺值、尚未公布、STALE/ERROR/N/A 的處理是否會誤當成 0。
- 2026-09-29 `TPEX_3INSTI_HTML` before/after 是否為可確認的同日修訂、是否保留雙版本可 replay。
- 五日 Raw 與當前簡化版 `Fetch → Normalize → Store → Analyze → Verify` 規則是否有重大不相容或資料品質 blocker。
- 分析規格是否有造成錯誤投資判讀的重大風險；不要把單一 backfill 分析 sample 誤認成五日完整 normalized/report 歷史。

## 特別排除

- 不把長期 **00:00 / 07:00 unattended scheduler reliability** 當作目前進階 Gate；它是後續真實排程週期的獨立觀察。
- 不把 Legacy A2、Natural Sample、A6 或舊 Gate A 文件恢復為新流程的必要條件。
- 不為了形式完整要求無限增加樣本、文件、追蹤指標或新治理機制。
- 不把 metadata 空值自動推論為錯誤；需判斷該來源日期是否應具值，並指出具體風險。

## 請提供唯一 Overall Verdict

- `PASS`：可前進。
- `PASS_WITH_FOLLOW_UP`：**可前進**，非阻擋改善列入 backlog。
- `CORRECTIVE_REQUIRED`：已證實重大缺陷，需最小修正與針對性重驗。
- `INSUFFICIENT_EVIDENCE`：指出缺少的**精確來源、檔案、日期或證據**，不可泛稱「樣本不足」後要求重做架構。

對每個 finding 請列：`ID / Severity(BLOCKING, IMPORTANT, FOLLOW_UP) / Public GitHub evidence path / 可重現證據 / 為何影響結論 / 最小修復 / targeted retest 範圍`。

最後必須回答：

**「這個專案現在可以進入下一階段嗎？如果不行，真正阻擋的是哪個可重現缺陷？」**
