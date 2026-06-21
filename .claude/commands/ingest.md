# /ingest — 解析甲方文件至知識庫

## 觸發
```
/ingest                          （解析 _inbox/ 所有新文件）
/ingest [路徑或貼上文字]         （指定來源）
/ingest --batch                  （強制分批）
/ingest --batch-size=N           （每批頁數，預設 35）
/ingest --skip-appendix          （跳過附錄）
```

## 前置條件
- 若指定專案：`projects/{名稱}/` 必須存在（若無：提示先執行 `/project-init`）
- `knowledge/_schemas/req.md` 可讀（Phase 3 格式驗證用）

## ⚠️ 核心原則
解析與寫入分開。使用者確認前，**不寫入** `01-requirements/`。

---

## 執行序列（每次只讀當前 Phase 的子文件）

| 步驟 | 讀取 | 說明 |
|------|------|------|
| 0 | `.claude/commands/_ingest/detect.md` | 偵測輸入類型，路由至對應前處理 |
| 1 | `.claude/commands/_ingest/parse.md` | Phase 1：解析（只讀，不寫）|
| 2 | `.claude/commands/_ingest/confirm.md` | Phase 2：呈現確認報告 |
| 3 | `.claude/commands/_ingest/write.md` | Phase 3：寫入確認的內容 |
| 4 | `.claude/commands/_ingest/report.md` | Phase 4：完成回報 |

**特殊前處理（detect.md 指示時才讀）**

| 情況 | 子文件 |
|------|--------|
| 截圖 / Mockup / 流程圖 | `_ingest/input-visual.md` |
| CSV / Excel / 貼上表格 | `_ingest/input-structured.md` |
| 非中文文件 | `_ingest/input-multilang.md` |
| ≥ 30 頁 / ≥ 80,000 字元 | `_ingest/input-large.md` |
| 不確定歸屬哪個專案 | `_ingest/unassigned.md` |
| 涵蓋多個已知專案 | `_ingest/cross-project.md` |
