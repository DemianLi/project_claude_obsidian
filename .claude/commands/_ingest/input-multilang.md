# Phase 0-C：多語言文件處理

**適用**：文件全部或主要為非中文（英文 / 日文 / 其他）

---

## C-1：語言偵測說明

```
⚠️ 偵測到文件語言：{英文 / 日文 / 其他}

本知識庫工作語言為中文。解析過程將同步翻譯：
① 需求寫入知識庫時以中文為主
② 每條需求保留「原文」欄位（原句）
③ 技術/業務術語自動標記「建議加入中英對照」

繼續？(Y/n)
```

## C-2：翻譯 + 術語識別（貫穿 Phase 1）

Phase 1 解析時同步執行：
- 將每條需求翻譯為中文，保留原文
- 標記需要中英對照的詞彙：
  ```
  識別到術語：
    "Invoice reconciliation" → 發票對帳（建議加入 domain-knowledge.md）
    "Settlement period"      → 結算週期（建議加入 domain-knowledge.md）
  ```

## C-3：Phase 2 雙語格式

```
[1] 使用者可用 email 和密碼登入系統
    原文：Users can log in with email and password
    驗收：登入成功跳轉首頁，失敗顯示錯誤訊息
    → 確認寫入？ (Y/n)
```

## C-4：REQ 格式新增欄位

```markdown
**來源文件**：{文件名}（原文語言：English）
**原文**：{原句}
```

## C-5：術語寫入 domain-knowledge.md（Phase 3 後詢問）

```
以下術語建議加入 domain-knowledge.md 中英對照：
  Invoice reconciliation → 發票對帳
  Settlement period      → 結算週期
要現在寫入嗎？(Y/n)
```

→ 與 `_ingest/parse.md` 並行執行（C-2 嵌入 Phase 1 內）
