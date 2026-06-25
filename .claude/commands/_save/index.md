# Phase 2：更新 wiki + 維護薄索引（自動執行）

## Step 4：更新 wiki/hot/{engineer}.md（完整替換自己的檔案）

工程師縮寫從 `.claude/collab/{initials}.md` 讀取；若無 collab 資料則詢問縮寫或預設 `default`。
每位工程師只替換自己的檔案，其他人的 hot 檔案不動。

```markdown
## 🔄 最近工作（{日期}）｜{engineer}

**活躍專案**：{專案名}
**上次工作**：{YYYY-MM-DD}

### 本次完成
- {完成項目}

### 進行中
- {還在做的}

### 待辦（下次繼續）
- {未完成}

### 重要決策
- {記錄重要決策}

### 注意事項
- {下次需要記住的事}
```

## Step 5：Append wiki/log.md

```
### [{日期}] {專案} — {一句話摘要}
- {完成項目}
- {重要決策}
- {遺留問題}
```

## Step 8：維護索引與 Quick Context（自動執行，不需確認）

| 更新目標 | 更新內容 | 條件 |
|----------|---------|------|
| `functional-index.md` | 更新需求數統計、模組狀態摘要 | 本次有新增或修改 REQ |
| `ADR-index.md` | Append 新 ADR 一行摘要 | 本次建立新 ADR |
| `05-dev-notes/_index.md` | Append 今日 session 一行摘要（日期/REQ/工時/標籤） | 本次有 dev-notes |
| `bugs-active.md` | 移除已關閉 bug；更新統計摘要 | 本次有關閉 bug |
| `_pending/_index.md` | 更新 QUICK CONTEXT 頭（阻塞數/總數） | 本次有新增或解決 PENDING |
| `_inferred/_index.md` | 更新 QUICK CONTEXT 頭（高風險數/GAP 數） | 本次有新增或升格 INF/GAP |
| 各文件的 `## 📌 Quick Context` | 更新本次修改過文件的 Quick Context 區塊 | 文件內容有異動 |

Quick Context 更新格式：
```
## 📌 Quick Context
| 欄位 | 內容 |
|------|------|
| **[關鍵欄位]** | {本次 session 後的最新狀態} |
| **最後更新** | {今日日期} |
```

→ 完成後讀取 `_save/report.md`
