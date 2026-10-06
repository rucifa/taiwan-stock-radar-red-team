# LEGACY MIGRATION NOTE

## 1. Purpose

本文件只處理舊 A2／Gate A／Natural Sample 架構與新每日市場雷達流程的邊界。

## 2. 新正式日常流程

新日常流程只保留：

- 00:00：**Fetch + Store + Analyze**
- 07:00：**Verify + Repair**

新流程目的：

> **可靠保存資料 + 每日分析**

## 3. 舊 A2 保留方式

以下全部保留為歷史紀錄：

- A2 Scheduler Policy
- Natural Sample
- Primary / Recovery
- Recovery contamination
- activation boundary
- A6 attestation
- Gate A historical manifests / evidence
- historical corrective audit / red-team evidence

不得刪除、retroactively rewrite 或 retroactively reclassify 舊 evidence。

## 4. 新流程不再要求

每日抓取／保存／市場雷達分析不再需要以下 gate：

- Natural eligibility
- Primary provenance
- Recovery contamination
- A6 closure
- Gate A readiness
- external automation attestation

只有使用者明確要求研究 Legacy A2 時才使用。

## 5. 新舊資料共存

舊 `archive/`、`manifests/`、`evidence/` 可繼續保留。

新每日正式資料採：

- `data/daily/YYYY/YYYY-MM-DD.json`
- `reports/daily/YYYY/YYYY-MM-DD.md`
- `state/latest.json`

不要求把所有歷史 Raw 重新搬家。

## 6. Conflict Rule

若舊 A2 文件與三份新核心文件對「新日常流程」的描述衝突：

> **以 `README_FIRST.md`、`DAILY_MARKET_RADAR_SPEC.md`、`MARKET_RADAR_ANALYSIS_SPEC.md` 為準。**

若問題是「舊 A2 當時究竟如何定義」，仍以舊 A2 canonical evidence 為準，不用新文件回寫歷史。
