---
type: meta
title: "Questions Index"
updated: 2026-06-22
---

# 問答歸檔索引

> 此資料夾存放 `/query deep:` 或值得保留的查詢答案。
> 好的答案在這裡複利增長——下次問同樣問題時直接從快取回答。

## 歸檔條件（符合任一即歸）

- 答案整合了 3 個以上來源
- 答案花了超過 5 分鐘才得出
- 這個問題大概率下次還會問到
- 答案包含決策建議（不只是事實陳述）

## 頁面格式

```yaml
---
type: question
title: "問題簡述"
question: "原始問題完整文字"
answer_quality: draft | solid | definitive
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [domain, subtag]
related:
  - "[[引用頁面]]"
sources:
  - "[[wiki/sources/來源頁面]]"
---
```

## 架構與設計決策
<!-- 例：[[為什麼用軟刪除而非硬刪除]], [[API 版本策略比較]] -->

## 技術選型
<!-- 例：[[Redis vs Memcached 快取選型]], [[MySQL vs PostgreSQL 在台灣甲方場景]] -->

## 甲方溝通
<!-- 例：[[如何說明需求變更對工時的影響]] -->

---
*共 0 頁 | 最後更新：2026-06-22*
