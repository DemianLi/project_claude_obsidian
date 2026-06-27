# /query [問題] — 查詢模式

## 查詢深度路由

| 觸發 | 模式 | Token 預算 | 適用 |
|------|------|-----------|------|
| `/query quick: [問題]` | Quick | ~1,500 | 快速事實、日期、簡單定義 |
| `/query [問題]`（預設） | Standard | ~3,500 | 大多數查詢 |
| `/query deep: [問題]` | Deep | ~8,000+ | 跨多來源綜合分析、比較 |

---

## Quick 模式

1. 讀 `wiki/hot/*.md` → 若有答案，直接回覆，**停止**
2. 讀 `wiki/index.md` → 掃描描述，若找到答案，回覆，**停止**
3. 若均無 → 回覆「Quick 快取沒有此資訊，要切換為 Standard 查詢嗎？」

不開啟任何個別頁面。

---

## Standard 模式（預設）

### Step 1：宣告 Routing 決策（不讀任何檔案）

**先輸出以下宣告，等使用者確認後才讀檔：**

```
📍 Routing 決策
問題類型：{類型}
將讀取：{目標路徑}
理由：{一句話}

確認正確請按 Enter，或告訴我正確方向。
```

| 問題類型 | 目標路徑 |
|----------|----------|
| 功能需求 | `{KB_ROOT}/projects/{名稱}/01-requirements/functional-index.md` → 對應 REQ |
| 甲方系統限制 | `{KB_ROOT}/projects/{名稱}/03-client-context/existing-system.md` |
| 術語 / 領域知識 | `{KB_ROOT}/projects/{名稱}/03-client-context/domain-knowledge.md` + `{KB_ROOT}/wiki/concepts/` |
| 技術決策原因 | `{KB_ROOT}/projects/{名稱}/04-decisions/ADR-index.md` → 對應 ADR |
| 可複用解法 | `{KB_ROOT}/knowledge/patterns/index.md` |
| 歷史踩坑 | `{KB_ROOT}/knowledge/lessons-learned/index.md` |
| 技術 / 服務知識 | `{KB_ROOT}/wiki/entities/_index.md` + `{KB_ROOT}/knowledge/tech-stack/index.md` |
| 概念定義 | `{KB_ROOT}/wiki/concepts/_index.md` → 對應概念頁 |
| 過去研究 | `{KB_ROOT}/wiki/sources/_index.md` + `{KB_ROOT}/wiki/questions/_index.md` |

若問題跨多類型，列出**所有**預計讀取路徑讓使用者確認，避免遺漏或多讀。

### Step 2：讀取並合成（最多 3-5 頁）

- 引用具體來源（「根據 REQ-F003」「根據 ADR-002」「根據 [[Redis 實體頁]]」）
- 遵循熱快取讀取順序：hot/*.md → index → 目標頁（若 hot/*.md 有答案即停止）
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

1. 讀 `wiki/hot/*.md` + `wiki/index.md`（建立全局視圖）
2. 識別所有相關節點（concepts/entities/sources/questions + projects/knowledge/）
3. 開啟所有相關頁面，深讀，不設上限
4. 若 wiki 覆蓋薄 → 詢問「要補充 web search 嗎？」（可銜接 `/research`）
5. 輸出綜合分析 + 完整引用
6. **一定**歸檔至 `wiki/questions/`（Deep 答案太有價值不能只留在 chat）
