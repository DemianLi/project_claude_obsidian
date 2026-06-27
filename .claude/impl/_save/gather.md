# Phase 1：彙整 Session 內容

## Step 1：彙整本次 Session 內容

回顧對話，提取：
- 完成了哪些功能/任務
- 做了哪些重要技術決策
- 遇到了哪些問題和解法
- 發現了哪些需求變更或新需求
- 目前的阻塞點或待辦

## Step 2：建立 Dev Session 筆記

若有實質開發內容，在 `projects/{專案}/05-dev-notes/` 建立：
`YYYY-MM-DD-{主題摘要}.md`（套用 `_templates/dev-session.md`）

詢問：「本次 session 大約花了多少小時？實作的哪個需求（REQ-ID）？」

## Step 3：建立新的 ADR（若需要）

若本次有重要技術決策尚未記錄，詢問：
「本次對話中有以下決策點，要建立 ADR 記錄嗎？」
- {識別出的決策點列表}

## Step 6：掃描背景知識更新

| 發現類型 | 詢問方式 |
|----------|----------|
| 新的關係人資訊（新聯絡人、偏好改變） | 「本次發現 {人名} 的新偏好，要更新 stakeholders.md？」 |
| 現有系統新資訊（技術限制、整合點） | 「本次確認了 {技術細節}，要更新 existing-system.md？」 |
| 領域知識（術語、業務規則、法規） | 「本次理解了 {概念}，要記錄至 domain-knowledge.md？」 |

## Step 4：協作狀態更新（條件）

若 `{KB_ROOT}/projects/{專案名稱}/collab/` 存在 → 讀 `{KB_ROOT}/.claude/impl/_collab/update.md` 執行鎖定更新。
若不存在 → 跳過。

## Step 7：掃描教訓、模式與第三方服務坑

- 新教訓 → 詢問是否更新 `knowledge/lessons-learned/`
- 可複用模式 → 詢問是否更新 `knowledge/patterns/`
- 第三方服務發現 → **主動詢問**：
  「本次有串接 {服務名稱}，是否有新踩到的坑或有效配置要記錄到 tech-stack/？」

→ 完成後讀取 `_save/index.md`
