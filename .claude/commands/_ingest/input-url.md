# Phase 0-F：URL 輸入前處理

觸發條件：輸入為 `https://` 開頭的 URL。

---

## Step F-1：抓取網頁

使用 WebFetch 抓取 URL 內容。

若抓取失敗（需要登入 / 被封鎖 / 空白內容）→ 告知使用者，請求提供替代來源（截圖或複製文字）。

---

## Step F-2：衍生 slug

從 URL 路徑衍生檔名 slug：
- 取 URL 最後路徑段
- 全小寫、空格 → 連字號、移除查詢字串
- 例：`https://redis.io/docs/data-types/` → `data-types`

---

## Step F-3：存入 .raw/

```markdown
---
source_url: {URL}
fetched: {YYYY-MM-DD}
type: web-article
---

{抓取的內容}
```

存至：`.raw/articles/{slug}-{YYYY-MM-DD}.md`

若 `.raw/articles/` 不存在 → 自動建立。

---

## Step F-4：更新 Delta Manifest

在 `.raw/.manifest.json` 記錄此來源：
```json
{
  "sources": {
    ".raw/articles/{slug}-{YYYY-MM-DD}.md": {
      "origin_url": "{URL}",
      "fetched": "{YYYY-MM-DD}",
      "hash": "{md5 of content}",
      "ingested_at": null
    }
  }
}
```
（`ingested_at` 在 Phase 4 完成後補填）

若 `.manifest.json` 不存在 → 建立新檔。

---

## Step F-5：判斷語言

若網頁內容主要為非中文 → 同時觸發 `input-multilang.md`（0-C）Phase 0-C 的翻譯流程。

---

## Step F-6：進入標準流程

→ 前往 `_ingest/parse.md`（Phase 1）
（來源檔為剛存入的 `.raw/articles/{slug}.md`）

---

## wiki/sources/ 頁面（Phase 3 寫入時建立）

URL 來源解析完成後，在 `wiki/sources/` 建立摘要頁：

```markdown
---
type: source
title: "{頁面標題}"
source_url: {URL}
fetched: {YYYY-MM-DD}
status: developing
tags: [source, {domain}]
related:
  - "[[相關實體或概念]]"
---

# {頁面標題}

**來源**：[{URL}]({URL})
**抓取日期**：{YYYY-MM-DD}

## 關鍵洞見

{3-5 條最重要的內容摘要}

## 提取實體

{[[實體1]], [[實體2]]...}

## 提取概念

{[[概念1]], [[概念2]]...}
```

更新 `wiki/sources/_index.md` 和 `wiki/index.md`。
