# 知識庫寫入規則

## 操作規則

| 操作 | 規則 |
|------|------|
| `/ingest` 解析 | Phase 1-2 只讀分析，Phase 3 才寫入，且只寫使用者確認的項目 |
| 模糊需求 | 不寫入 `functional/{module}.md`，只存 `_pending/{ID}.md` |
| 需求衝突 | 不自動覆寫，等待使用者裁決 |
| ADR | 只記錄已做出的決策，不記錄「考慮中」的選項為決策 |
| 格式驗證 | 寫入任何 REQ / ADR / PAT / LESSON 前，先確認符合 `knowledge/_schemas/` 對應 schema 的必填欄位 |

## 衝突優先序

`functional/{module}.md`（✅ 確認）> `_pending/{ID}.md`（🕐 待確認）> `_inferred/{ID}.md`（🔍 推測）

## 重複資訊衝突處理

| 情況 | 行為 |
|------|------|
| functional/{module}.md 有確認版，_pending/{ID}.md 有舊模糊版 | 以確認版為準，**回報**：「PENDING-XXX 可能已被 REQ-FXXX 解決，請確認是否清理」 |
| functional/{module}.md 有確認版，_inferred/{ID}.md 有推測版 | 以確認版為準，**回報**：「INF-XXX 與 REQ-FXXX 語意重疊，建議 /reconcile」 |
| 兩個確認需求語意重疊 | **停止**，請使用者裁決哪一條為準 |
| _pending/ 內部有重複 | 繼續作業但回報：「PENDING-XXX 和 PENDING-YYY 可能是同一問題，建議 /reconcile 合併」 |

發現重複時**不靜默**，一律回報。

## Claude 自主邊界

| 可自主執行 | 必須等待使用者確認 |
|-----------|-----------------|
| 更新 `wiki/hot.md`、append `wiki/log.md` | 任何寫入 `functional/{module}.md` 的需求 |
| 格式整理、摘要彙整 | 任何刪除或覆寫既有知識庫記錄 |
| 識別衝突並回報 | 任何技術架構決策 |
| 提出選項清單 | 推測業務邏輯為事實 |
