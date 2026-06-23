# /query [問題] — 查詢模式

## 查詢深度路由

| 觸發 | 模式 | Token 預算 | 適用 |
|------|------|-----------|------|
| `/query quick: [問題]` | Quick | ~1,500 | 快速事實、日期、簡單定義 |
| `/query [問題]`（預設） | Standard | ~3,500 | 大多數查詢 |
| `/query deep: [問題]` | Deep | ~8,000+ | 跨多來源綜合分析、比較 |

---

## Quick 模式

1. 讀 `wiki/hot.md` → 若有答案，直接回覆，**停止**
2. 讀 `wiki/index.md` → 掃描描述，若找到答案，回覆，**停止**
3. 若均無 → 回覆「Quick 快取沒有此資訊，要切換為 Standard 查詢嗎？」

不開啟任何個別頁面。

---

## Standard 模式（預設）

### Step 1：問題層次判斷

| 問題類型 | 優先讀取 |
|----------|----------|
| 「這個功能的需求是什麼？」 | `01-requirements/functional-index.md` → 對應 REQ |
| 「甲方系統有什麼限制？」 | `03-client-context/existing-system.md` |
| 「這個術語是什麼意思？」 | `03-client-context/domain-knowledge.md` + `wiki/concepts/` |
| 「我們當初為什麼選 X？」 | `04-decisions/ADR-index.md` → 對應 ADR |
| 「有沒有類似的解法？」 | `knowledge/patterns/index.md` |
| 「這種情況之前踩過坑嗎？」 | `knowledge/lessons-learned/index.md` |
| 「關於 {技術/服務} 的知識」 | `wiki/entities/_index.md` + `knowledge/tech-stack/index.md` |
| 「{概念} 是什麼？」 | `wiki/concepts/_index.md` → 對應概念頁 |
| 「以前研究過 {主題} 嗎？」 | `wiki/sources/_index.md` + `wiki/questions/_index.md` |

### Step 2：讀取並合成（最多 3-5 頁）

- 引用具體來源（「根據 REQ-F003」「根據 ADR-002」「根據 [[Redis 實體頁]]」）
- 遵循熱快取讀取順序：hot.md → index → 目標頁（若 hot.md 有答案即停止）
- 若知識庫無答案 → 明確說「知識庫沒有這方面記錄」，不憑空猜測

### Step 3：缺口揭露

若問題揭露了知識庫中缺少的資訊：
```
💡 此資訊知識庫目前沒有記錄。
建議：
  - 有文件/URL → 執行 `/ingest [來源]` 解析進來
  - 需要搜尋 → 執行 `/research [主題]` 知識庫約束式搜索
  - 是術語 → 直接補充至對應 domain-knowledge.md 或 wiki/concepts/
```

### Step 4：歸檔建議（符合任一條件時詢問）

若此次回答：整合了 3 個以上來源 / 花了較長時間推導 / 包含決策建議
→ 主動問：「這個答案值得歸檔至 wiki/questions/ 嗎？」

若使用者同意，寫入 `wiki/questions/{問題slug}.md`：
```yaml
---
type: question
title: "{問題簡述}"
question: "{原始問題}"
answer_quality: solid
created: {YYYY-MM-DD}
updated: {YYYY-MM-DD}
tags: [{domain}]
related:
  - "[[引用頁面]]"
sources:
  - "[[wiki/sources/來源]]"
---
{答案完整內容}
```
更新 `wiki/questions/_index.md` 和 `wiki/index.md`。

---

## Deep 模式

1. 讀 `wiki/hot.md` + `wiki/index.md`（建立全局視圖）
2. 識別所有相關節點（concepts/entities/sources/questions + projects/knowledge/）
3. 開啟所有相關頁面，深讀，不設上限
4. 若 wiki 覆蓋薄 → 詢問「要補充 web search 嗎？」（可銜接 `/research`）
5. 輸出綜合分析 + 完整引用
6. **一定**歸檔至 `wiki/questions/`（Deep 答案太有價值不能只留在 chat）
