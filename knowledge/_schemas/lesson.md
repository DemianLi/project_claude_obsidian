---
type: schema
entity: LESSON
version: 1.0
updated: 2026-06-21
---

# Schema：LESSON（教訓）

> `/self-improve` Phase 4、`/save` 步驟 7 以此為格式參考。

---

## 完整格式

一條 LESSON 一個獨立檔案（`knowledge/lessons-learned/LESSON-{NNN}.md`），frontmatter 在檔案最前面：

```markdown
---
tags: [{tag1}, {tag2}]
phase: requirements | development | testing | delivery | communication
root_cause: misunderstanding | technical | process | communication | estimation
severity: 🔴 高（直接影響交付）| 🟡 中（影響品質或效率）| 🟢 低（輕微影響）
status: active | superseded | context-specific
---

# LESSON-{NNN}：{簡短標題（動詞+名詞，描述問題）}

**來源專案**：{專案名}（若通用則填「通用」）
**發生情境**：{什麼情況下發生——場景描述，1-2 句）
**問題描述**：{實際發生了什麼——結果描述}
**根本原因**：{為什麼發生——系統性原因，不是單次失誤}
**預防方式**：{下次怎麼避免——具體可執行的步驟}
**偵測信號**：{早期跡象——讓你能在問題爆發前發現它}
**實際工時損失**：{N} 小時（因此問題導致的額外工時；若不確定填「未記錄」）

## 是否已納入系統守衛？

- [ ] 尚未納入自動檢查
- [ ] 已納入 BEFORE CODING 步驟 {N}
- [ ] 已納入 `/ingest` 的衝突偵測

## 相關資源

- **相關 Pattern**：{PAT-XXX（若有對應的正向解法）}
- **相關需求守衛**：{說明這個教訓如何體現在 CLAUDE.md 的哪條規則中}
```

---

## 有效欄位值

### phase（問題發生在哪個階段）

| 值 | 說明 |
|----|------|
| `requirements` | 需求收集、確認、解讀階段 |
| `development` | 實作、架構設計階段 |
| `testing` | QA、UAT、測試計畫 |
| `delivery` | 交付、部署、驗收 |
| `communication` | 與甲方或團隊的溝通問題 |

### root_cause（問題根因分類）

| 值 | 說明 |
|----|------|
| `misunderstanding` | 對需求或術語的誤解 |
| `technical` | 技術知識不足或技術選型錯誤 |
| `process` | 流程或步驟不完整 |
| `communication` | 溝通不清楚或缺乏確認 |
| `estimation` | 工時或複雜度估算錯誤 |

### status

| 值 | 說明 |
|----|------|
| `active` | 仍有效，應繼續避免 |
| `superseded` | 已有更好的防範措施，由 {LESSON-XXX} 取代 |
| `context-specific` | 只在特定技術棧或甲方環境下成立 |

---

## 健康檢查規則（供 /health-check 使用）

一個 LESSON 被視為「不健康」如果：
- 缺少 `tags`
- 缺少 `phase` 或 `root_cause`
- 缺少「預防方式」（這是最重要的欄位）
- 缺少「偵測信號」
- 「是否已納入系統守衛」未填
