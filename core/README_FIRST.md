# 台股投資雷達｜README FIRST

## 1. 專案唯一目的

本專案只處理兩件事：

1. **可靠保存每日台股市場資料到 GitHub**
2. **由 ChatGPT 根據保存資料完成每日市場雷達分析**

Private GitHub Repository：

`<PRIVATE_PRODUCTION_REPOSITORY>`

Branch：

`main`

GitHub 的主要定位是：

> **Daily Market Data Storage + Historical Data Source**

不再把 A2 Natural Sample、Primary / Recovery、Recovery contamination、activation boundary、A6 attestation 等歷史治理機制作為每日流程的必要條件。

---

## 2. 每次工作開始時的讀取順序

固定優先閱讀：

1. `README_FIRST.md`
2. `DAILY_MARKET_RADAR_SPEC.md`
3. `MARKET_RADAR_ANALYSIS_SPEC.md`

只有在處理舊 A2／歷史架構／舊 evidence 時，才讀：

4. `LEGACY_MIGRATION_NOTE.md`

若聊天記憶、舊 Prompt、舊 A2 文件與上述核心文件衝突，以核心文件最新版本為準。

---

## 3. 正式每日排程

### Asia/Taipei 00:00｜週二～週六

同一次 Automation 完成：

**Trading-Day Resolve  
→ 抓取官方市場資料  
→ 正規化  
→ 寫入 GitHub  
→ 讀取歷史資料  
→ 計算衍生指標  
→ 完成每日市場雷達  
→ 保存分析報告  
→ 輸出使用者可見結果**

不再拆成 00:00 Capture 與 01:00 Radar。

### Asia/Taipei 07:00｜週二～週六

執行：

**Verify  
→ 找出 Missing / Delayed / Stale data  
→ 必要時重新抓取官方資料  
→ 更新 GitHub  
→ 重算受影響的 derived metrics**

只有修正足以改變下列任一判斷時，才更新完整市場雷達：

- Market Regime
- 雷達總分
- 追加機會等級
- 今日新增投入
- 建議投入比例
- All-in 適合度

否則只回報：

> **07:00 驗證完成；資料已確認／補齊，市場雷達無需修改。**

---

## 4. 資料來源

優先順序：

**TWSE / TPEx / TAIFEX  
→ 其他正式官方來源  
→ 必要時才使用可靠非官方補充來源**

不得使用較早交易日資料冒充 target business date。

資料尚未公布或取得失敗時標記：

- `MISSING`
- `NOT_PUBLISHED`
- `STALE`
- `ERROR`
- `N/A`

不得自行捏造或估算。

---

## 5. GitHub 正式資料結構

每日資料：

`data/daily/YYYY/YYYY-MM-DD.json`

每日分析報告：

`reports/daily/YYYY/YYYY-MM-DD.md`

最新狀態：

`state/latest.json`

只有 GitHub write 成功後，才可宣稱資料已保存。

單一來源失敗時仍保存 partial record；不得因一個來源失敗讓整個交易日資料消失。

---

## 6. 市場雷達投資原則

主要長期標的：

- 0050
- 006208
- 00981A

用途為長期退休資產累積。

固定原則：

- 原定定期定額照常。
- 不提供短線賣出訊號。
- 雷達主要判斷 Market Regime、風險與額外加碼機會。
- 額外投入只使用「額外可投入資金池」。
- 不得建議動用生活緊急預備金。
- 使用者偏好 Lump Sum / All-in，不要為分批而分批。

完整評分與輸出規則以 `MARKET_RADAR_ANALYSIS_SPEC.md` 為準。

---

## 7. Legacy A2

舊 A2 policy、Natural Sample、Primary / Recovery、Recovery contamination、A6、歷史 manifests / evidence 全部保留為歷史紀錄。

不得 retroactively rewrite 舊 evidence。

但除非使用者明確要求處理 Legacy A2：

> **不得再讓舊 A2 治理成為每日抓取、保存或市場雷達分析的 gate。**

---

## 8. 設計優先順序

當多種方式都可完成需求時，依序優先：

1. 正確
2. 穩定
3. 簡單
4. 可維護
5. 可追溯
6. 最後才增加治理複雜度
