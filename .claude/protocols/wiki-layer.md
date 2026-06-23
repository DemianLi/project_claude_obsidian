# Obsidian Wiki 層協議

此文件定義 wiki 知識層（concepts/entities/sources/questions）的寫入慣例。
工程層（projects/ knowledge/）不受此文件約束，依各自格式規範。

---

## Frontmatter（每個 wiki 頁面必填）

```yaml
---
type: concept | entity | source | question
title: "頁面標題"
status: seed | developing | stable | stale
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [domain, subtag]
related:
  - "[[相關頁面]]"
---
```

- `seed`：初建，內容最小化
- `developing`：正在擴充中
- `stable`：完整，短期不會大改
- `stale`：可能過時，需要重新驗證

---

## Wikilinks

使用 `[[頁面名稱]]` 格式建立連結，檔名全庫唯一（不需路徑）。
每次提到已有 wiki 頁面的概念/實體，必須連結。

---

## Callout 類型（`.obsidian/snippets/vault-colors.css` 定義）

詳細 schema 見 `knowledge/_schemas/callouts.md`。

| Callout | 用途 |
|---------|------|
| `> [!contradiction]` | 此頁聲明與另一頁衝突，需人工裁決 |
| `> [!gap]` | 知識缺口，尚未找到資料 |
| `> [!key-insight]` | 重要洞見，高度強調 |
| `> [!stale]` | 此段資訊可能已過時 |

---

## 資料夾結構與用途

| 資料夾 | 內容 | 更新時機 |
|--------|------|----------|
| `wiki/concepts/` | 概念、框架、設計模式 | 學到新概念時 |
| `wiki/entities/` | 工具、服務、技術（如 Redis、LINE Pay） | 首次使用或重要發現時 |
| `wiki/sources/` | 文章/文件/研究資料摘要 | `/ingest` 解析後 |
| `wiki/questions/` | 查詢後值得保留的答案 | `/query` 回答後主動歸檔 |

---

## 更新規則

- `wiki/index.md`：每次新增 wiki 頁面時更新（append 該頁摘要）
- `wiki/log.md`：每次 ingest / 大量更新後 append（新條目置頂）
- `wiki/hot.md`：Session 結束時完整替換（≤500 字）
- `.raw/`：**不可修改**，只讀——原始輸入文件保存處

---

## wiki 層 vs 工程層 界線

| 內容類型 | 放哪裡 |
|----------|--------|
| 技術概念、框架理解 | `wiki/concepts/` |
| 第三方服務踩坑 | `knowledge/tech-stack/` + `wiki/entities/{服務}.md` |
| 甲方專案需求 | `projects/{名稱}/01-requirements/` |
| 可複用設計模式（跨專案） | `knowledge/patterns/` |
| 閱讀筆記、研究摘要 | `wiki/sources/` |
| 業務術語（特定甲方） | `projects/{名稱}/03-client-context/domain-knowledge.md` |
| 通用術語（跨甲方） | `wiki/concepts/` |
