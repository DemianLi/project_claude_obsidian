# Phase 4：更新知識庫索引

## 4-1. 更新 wiki/index.md

將此專案從「🔄 進行中」移至「✅ 已完成」：

```markdown
## ✅ 已完成

### {專案名稱}（完成：{YYYY-MM-DD}）
- **甲方**：{甲方名稱}
- **交付版本**：{版本號}
- **最終需求數**：{N} 條（含 {M} 條 CR 追加）
- **交付文件**：`projects/{專案}/06-qa-testing/delivery-doc-v{版本}.md`
- **技術交接文件**：`projects/{專案}/handover-doc-{日期}.md`（若有）
```

## 4-2. 更新 wiki/hot/{自己的縮寫}.md

從「活躍專案」移除此專案，改為「最近完成」：

```markdown
### 最近完成
- {專案名稱}（{YYYY-MM-DD} 結案）— 備注：{交付版本}
```

## 4-3. Append wiki/log.md

```
### [{日期}] {專案名稱} — 專案結案
- 交付版本：{版本}
- 需求完成數：{N}/{Total}
- 交付文件已生成
- 遺留問題：{N} 個（已記錄於 CHANGELOG）
```

→ 完成後讀取 `_close-project/archive.md`
