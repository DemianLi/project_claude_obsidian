---
description: 解析甲方文件入庫（文字/URL/圖片/Excel，支援 --url --visual 等直接路由）
---
# /ingest — 解析甲方文件至知識庫

## 觸發
```
/ingest                          （解析 _inbox/ 所有新文件，自動偵測類型）
/ingest [路徑或貼上文字]         （指定來源，自動偵測類型）
/ingest --url [URL]              （直接跳到 URL 處理，跳過 detect）
/ingest --visual                 （直接跳到圖片/截圖處理，跳過 detect）
/ingest --structured             （直接跳到 CSV/Excel 處理，跳過 detect）
/ingest --multilang              （直接跳到多語言處理，跳過 detect）
/ingest --large                  （直接跳到大型文件分批，跳過 detect）
/ingest --unassigned             （直接跳到未知專案處理，跳過 detect）
/ingest --cross                  （直接跳到跨專案處理，跳過 detect）
/ingest --batch                  （強制分批）
/ingest --batch-size=N           （每批頁數，預設 35）
/ingest --skip-appendix          （跳過附錄）
```

## 前置條件
- 若指定專案：`{KB_ROOT}/projects/{名稱}/` 必須存在（若無：提示先執行 `/project-init`）
- `{KB_ROOT}/knowledge/_schemas/req.md` 可讀（Phase 3 格式驗證用）

## ⚠️ 核心原則
解析與寫入分開。使用者確認前，**不寫入** `01-requirements/`。

---

## 執行序列

### Step 0：解析 $ARGUMENTS → 直接路由（不詢問）

| $ARGUMENTS 包含 | 動作 |
|----------------|------|
| `--url` 或開頭為 `https://` | 直接讀 `{KB_ROOT}/.claude/impl/_ingest/input-url.md` |
| `--visual` | 直接讀 `{KB_ROOT}/.claude/impl/_ingest/input-visual.md` |
| `--structured` | 直接讀 `{KB_ROOT}/.claude/impl/_ingest/input-structured.md` |
| `--multilang` | 直接讀 `{KB_ROOT}/.claude/impl/_ingest/input-multilang.md` |
| `--large` | 直接讀 `{KB_ROOT}/.claude/impl/_ingest/input-large.md` |
| `--unassigned` | 直接讀 `{KB_ROOT}/.claude/impl/_ingest/unassigned.md` |
| `--cross` | 直接讀 `{KB_ROOT}/.claude/impl/_ingest/cross-project.md` |
| 以上皆無 | 讀 `{KB_ROOT}/.claude/impl/_ingest/detect.md`（自動偵測） |

上方 7 個旗標皆**跳過 detect**，直接進入對應 Phase 1。

### Step 1–4：標準 Phase 流程（每次只讀當前 Phase）

| 步驟 | 讀取 | 說明 |
|------|------|------|
| 1 | `{KB_ROOT}/.claude/impl/_ingest/parse.md` | Phase 1：解析（只讀，不寫）|
| 2 | `{KB_ROOT}/.claude/impl/_ingest/confirm.md` | Phase 2：呈現確認報告 |
| 3 | `{KB_ROOT}/.claude/impl/_ingest/write.md` | Phase 3：寫入確認的內容 |
| 4 | `{KB_ROOT}/.claude/impl/_ingest/report.md` | Phase 4：完成回報 |
