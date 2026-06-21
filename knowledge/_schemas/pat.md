---
type: schema
entity: PAT
version: 1.0
updated: 2026-06-21
---

# Schema：PAT（設計模式）

> `/self-improve`、`/save`、BEFORE CODING 步驟 7 以此為格式參考。

---

## 完整格式

```markdown
### PAT-{CATEGORY}-{NNN}：{模式名稱}

---
tags: [{tag1}, {tag2}, {tag3}]
status: validated | experimental | conditional | deprecated
projects: [{專案名}, {專案名}]
---

**驗證次數**：{N} 次（跨 {M} 個專案）
**適用情境**：{一句話描述什麼情況用這個模式}
**不適用情境**：{一句話描述什麼情況不要用}
**參考工時**：初次實作約 {X-Y} 小時；複用約 {A-B} 小時

#### 實作要點

{核心實作方式，用技術術語描述，2-5 個要點}

#### 注意事項

- {陷阱或限制一}
- {陷阱或限制二}

#### 相關資源

- **相關教訓**：{LESSON-XXX（若有對應踩坑記錄）}
- **相關 ADR**：{ADR-XXX（若有對應決策記錄）}
```

---

## ID 命名規則

格式：`PAT-{CATEGORY}-{NNN}`

| CATEGORY | 說明 |
|----------|------|
| `AUTH` | 認證與授權 |
| `DB` | 資料庫設計 |
| `API` | API 設計 |
| `UI` | 前端 / UI 設計 |
| `INFRA` | 基礎設施 / DevOps |
| `INTG` | 第三方整合 |
| `SEC` | 安全性 |
| `PERF` | 效能優化 |
| `DATA` | 資料處理 / ETL |

---

## 有效 status 值

| status | 含義 | Claude 在 BEFORE CODING 的處理 |
|--------|------|-------------------------------|
| `validated` | 至少在 2 個專案驗證有效 | 優先推薦使用 |
| `experimental` | 只在 1 個專案試用，尚未充分驗證 | 推薦但附警語「仍在觀察中」 |
| `conditional` | 在特定條件下有效（需說明條件） | 說明適用條件後再推薦 |
| `deprecated` | 有更好的替代方案 | 不推薦，若被引用則提醒遷移 |

---

## Tags 建議清單（非強制，只是建議詞彙）

```
# 技術類
authentication, authorization, jwt, session, oauth
database, sql, mysql, postgres, soft-delete, migration
api, rest, graphql, error-handling, pagination, versioning
cache, redis, queue, async, webhook
security, xss, sql-injection, rate-limit

# 業務場景類
order-management, payment, inventory, notification
approval-workflow, audit-log, file-upload, report

# 品質類
testability, error-handling, logging, performance
```

---

## 健康檢查規則（供 /health-check 使用）

一個 PAT 被視為「不健康」如果：
- 缺少 `tags`（至少 1 個）
- 缺少 `status` 或 status 不在有效值列表
- `validated` 或 `experimental` 狀態但 `projects` 是空陣列
- 缺少「適用情境」說明
- 缺少「注意事項」（至少 1 條）
