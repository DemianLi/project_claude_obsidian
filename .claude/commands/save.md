# /save — 儲存 Session 並更新熱快取

## 目的
Session 結束時儲存工作狀態、更新所有索引、確保下次載入脈絡完整。

## 執行序列（每次只讀當前 Phase 的子文件）

| Phase | 讀取 | 說明 | 需要詢問使用者？ |
|-------|------|------|-----------------|
| 1 | `_save/gather.md` | 彙整 session 內容 + 建立 dev-notes + ADR | ✅ 工時 / ADR / 背景知識 / 教訓模式 |
| 2 | `_save/index.md` | 更新 wiki + 維護所有薄索引 | 自動執行 |
| 3 | `_save/report.md` | 完成回報 | 自動 |

## 自主執行（不需詢問）
- Step 4 wiki/hot.md 更新（完整替換）
- Step 5 wiki/log.md append
- Step 8 所有薄索引維護（functional-index / ADR-index / dev-notes/_index / bugs-active / Quick Context）

## 必須詢問使用者
- Step 2 工時（「本次 session 大約花了多少小時？實作哪個需求 REQ-ID？」）
- Step 3 ADR（「有以下決策點，要建立 ADR 記錄嗎？」）
- Step 6 背景知識更新（stakeholders / existing-system / domain-knowledge）
- Step 7 教訓、模式與第三方服務坑
