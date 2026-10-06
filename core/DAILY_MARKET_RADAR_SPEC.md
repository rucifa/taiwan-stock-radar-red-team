# DAILY MARKET RADAR SPEC

## 1. Scope

本文件定義台股每日市場雷達的：

- 交易日解析
- 官方資料取得
- 正規化
- GitHub 保存
- 07:00 驗證／補修
- Partial data 行為
- Daily report 保存規則

分析與評分方法另見：

`MARKET_RADAR_ANALYSIS_SPEC.md`

---

# 2. Canonical Schedule

Timezone：`Asia/Taipei`

## 00:00｜Tue–Sat｜Fetch + Store + Analyze

每次執行同一個完整流程：

1. Resolve target date
2. 判斷 target date 是否為台股交易日
3. 抓取官方市場資料
4. 正規化
5. 保存 `data/daily/...json`
6. 讀取歷史資料
7. 計算 derived metrics
8. 執行 Market Radar Analysis
9. 保存 `reports/daily/...md`
10. 更新 `state/latest.json`
11. 輸出使用者可見結果

## 07:00｜Tue–Sat｜Verify + Repair

1. 讀取 target business date 的 daily JSON
2. 驗證來源日期、完整性與 freshness
3. 找出 `MISSING / NOT_PUBLISHED / STALE / ERROR`
4. 重新查官方來源
5. 若有新資料或正式修訂：更新 daily JSON 並重算受影響 derived metrics
6. 判斷是否足以改變市場雷達
7. 有重大影響才重寫 daily report；否則只輸出 Verify OK

---

# 3. Trading-Day Resolve

00:00 task 的 target date 原則為：

> **前一個日曆日**

由於排程只在週二～週六執行，通常對應週一～週五。

必須使用 TWSE 正式交易日／休市資訊判斷。

若 target date 為休市日：

- 不得拿更早交易日冒充
- 不建立新的交易日 daily JSON
- 不建立新的雷達分數
- 不解鎖新的額外投入
- 輸出「休市／無新交易資料」
- `state/latest.json` 保持最近有效交易日

---

# 4. Source Priority

來源優先順序：

1. TWSE
2. TPEx
3. TAIFEX
4. 其他政府／正式官方來源
5. 必要時可靠非官方來源補充

非官方資料不得覆蓋已取得的官方資料。

每個資料項目至少保存：

- `source_id`
- `source_type`
- `business_date`
- `as_of`
- `status`
- `value` 或正規化內容
- 必要時 `source_url` / provenance note

---

# 5. Required Status Vocabulary

- `PASS`：已取得且 target business date 正確
- `MISSING`：應有資料但未取得
- `NOT_PUBLISHED`：官方尚未公布
- `STALE`：取得資料但 business date / as-of 過舊
- `ERROR`：抓取或解析失敗
- `N/A`：該日／該項不適用

不得把 `MISSING / NOT_PUBLISHED / STALE / ERROR` 當成 0。

---

# 6. Daily JSON

正式路徑：

`data/daily/YYYY/YYYY-MM-DD.json`

建議最小結構：

```json
{
  "schema_version": "1.0",
  "business_date": "YYYY-MM-DD",
  "captured_at": "ISO-8601",
  "last_verified_at": "ISO-8601",
  "record_status": "COMPLETE|PARTIAL",
  "sources": {},
  "market": {},
  "breadth": {},
  "institutional": {},
  "margin": {},
  "derivatives": {},
  "international_context": {},
  "derived": {},
  "quality": {
    "data_confidence": "HIGH|MEDIUM|LOW",
    "missing_items": [],
    "not_published_items": [],
    "stale_items": [],
    "errors": []
  }
}
```

實際欄位可隨來源擴充，但不得破壞：

- business date 可追溯
- source/as-of 可辨認
- Missing 可辨認
- derived 與 raw/normalized data 可區分

---

# 7. Partial Record Rule

只要 target date 確認為交易日：

> **即使部分來源失敗，也必須保存 partial record。**

不得因單一來源失敗讓整日紀錄消失。

---

# 8. Historical / Derived Metrics

分析前讀取必要歷史資料，至少支援：

- 5 / 10 / 20 / 60 / 120 / 240 日均線
- 5 / 20 / 60 日均量
- 近期高點／一年高點回撤
- 外資 3 / 5 / 10 日
- 融資 1 / 5 / 20 日
- 台指期近 5 日（可得時）

若新 simplified daily database 尚不足形成長週期指標：

- 可讀取既有 GitHub 歷史資料
- 或從正式官方歷史資料補計算

但不得偽造缺失歷史。

---

# 9. Daily Report

路徑：

`reports/daily/YYYY/YYYY-MM-DD.md`

報告內容必須符合 `MARKET_RADAR_ANALYSIS_SPEC.md`。

只有報告實際寫入 GitHub 成功後，才可宣稱「報告已保存」。

---

# 10. state/latest.json

至少保存：

```json
{
  "latest_business_date": "YYYY-MM-DD",
  "daily_data_path": "data/daily/YYYY/YYYY-MM-DD.json",
  "daily_report_path": "reports/daily/YYYY/YYYY-MM-DD.md",
  "record_status": "COMPLETE|PARTIAL",
  "data_confidence": "HIGH|MEDIUM|LOW",
  "last_capture_at": "ISO-8601",
  "last_verified_at": "ISO-8601"
}
```

---

# 11. 07:00 Materiality Rule

只有修正足以改變以下任一結果時才重發完整市場雷達：

- Market Regime
- Radar Score
- 追加機會等級
- 今日新增投入
- 建議資金池投入比例
- All-in 適合度
- 關鍵 Data Confidence 且會影響判讀

若沒有實質改變：

> **只輸出簡短 Verify OK，不重複整份報告。**

---

# 12. Absolute Rules

- 不得拿上一交易日資料冒充 target date
- 不得自行估算未公布官方數據
- 不得因單一來源失敗而放棄整日保存
- GitHub write 成功後才能宣稱已保存
- 07:00 不為了「有更新」而硬改報告
- 舊 A2 governance 不得作為新日常流程 gate
