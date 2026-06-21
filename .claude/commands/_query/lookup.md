# /query [問題] — 一般查詢模式

## Step 1：解析問題層次

判斷問題屬於哪個層次，決定讀哪些檔案：

| 問題類型 | 優先讀取 |
|----------|----------|
| 「這個功能的需求是什麼？」 | `01-requirements/functional.md` |
| 「甲方的系統有什麼限制？」 | `03-client-context/existing-system.md` |
| 「這個術語是什麼意思？」 | `03-client-context/domain-knowledge.md` |
| 「我們當初為什麼選 X？」 | `04-decisions/` |
| 「有沒有類似的解法？」 | `knowledge/patterns/` |
| 「這種情況之前踩過坑嗎？」 | `knowledge/lessons-learned/` |

## Step 2：讀取並合成回答

- 引用具體來源（例：「根據 REQ-F003」「根據 ADR-002」）
- 若知識庫中無答案，明確說「知識庫中沒有這方面的記錄」，不憑空猜測
- 若問題涉及技術選型且知識庫沒有記錄 → 建議改用 `/research`

## Step 3：揭露知識庫缺口

若問題揭露了知識庫中缺少的資訊，主動說：
「這個資訊目前知識庫沒有記錄，要現在補充，還是執行 `/ingest` 整理進來？」
