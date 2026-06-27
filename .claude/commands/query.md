---
description: 查詢知識庫，三段深度：quick / standard / deep
---
# /query — 查詢知識庫

## 觸發方式
```
/query [問題]          （查詢知識庫中的既有記錄）
/query --verify        （驗證 Claude 對當前專案的理解是否正確）
/query --verify [主題] （針對特定主題驗證理解）
```

> 若需要查詢 + 網路搜索，請改用 `/research`。
> `/query` 只查知識庫內的記錄；`/research` 才會上網找新資料。

## 執行路由（每次只讀當前模式的子文件）

| 觸發 | 讀取 | 說明 |
|------|------|------|
| `/query [問題]` | `_query/lookup.md` | 解析問題層次 → 讀對應檔案 → 合成回答 |
| `--verify` / `--verify [主題]` | `_query/verify.md` | 主動暴露 Claude 的理解，請使用者確認或糾正 |

## 問題層次對照（lookup 模式快速參考）

| 問題類型 | 優先讀取 |
|----------|----------|
| 這個功能的需求是什麼？ | `01-requirements/functional.md` |
| 甲方的系統有什麼限制？ | `03-client-context/existing-system.md` |
| 這個術語是什麼意思？ | `03-client-context/domain-knowledge.md` |
| 我們當初為什麼選 X？ | `04-decisions/` |
| 有沒有類似的解法？ | `knowledge/patterns/` |
| 這種情況之前踩過坑嗎？ | `knowledge/lessons-learned/` |
