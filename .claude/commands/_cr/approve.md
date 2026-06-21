# /cr --approve CR-{N} — 核准變更請求

讀取 `04-decisions/CR-{N}-*.md`，執行以下步驟：

## Step 1：更新 scope.md 的追加範疇表

```markdown
| CR-{N} | {功能名稱} | {提出日期} | {提出人} | ✅ 已確認 | REQ-F{XXX} |
```

## Step 2：進入 /ingest 流程

將 CR 的需求描述視為已確認文件，執行完整的 `/ingest` 流程。

需求寫入 `functional.md` 時**合約版本欄位**標記為 `CR-{N}`。

## Step 3：更新 CR 文件狀態

```markdown
status: ✅ 已核准
**決策日期**：{YYYY-MM-DD}
**決策結果**：✅ 核准，列入追加範疇，合約版本 CR-{N}
```

## Step 4：完成回報

```
✅ CR-{N} 已核准

已新增至追加範疇（scope.md）
需求已進入 functional.md（標記 CR-{N}）

受影響需求：{列出 REQ ID}

建議：執行 /impact 確認無潛在衝突（若尚未執行）
```
