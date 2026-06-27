# Phase 5：生成健康度報告

彙整 Phase 1-4 的所有結果，輸出完整報告：

```
🏥 知識庫健康度報告
日期：{YYYY-MM-DD}｜掃描範圍：{N} 個進行中專案

━━━ 結構完整度 ━━━
{專案名}：{N}/10 ✅（{%}）
{專案名}：{N}/10 ⚠️（{%}）  缺少：{列表}

━━━ 格式合規性問題 ━━━
🔴 嚴重（{N} 個）：
  {專案}/{檔案}：{REQ-ID} 缺少「驗收條件」
🟡 警告（{N} 個）：
  {專案} _pending/{ID}.md：{PENDING-ID} 缺少「阻塞性」欄位

━━━ 孤立與過期問題 ━━━
（彙整 Phase 3 結果）

━━━ 知識庫健康統計 ━━━
（彙整 Phase 4 結果）

━━━ 建議優先處理 ━━━
🔴 最高優先（今天）：
  1. {具體問題 + 可直接執行的動作}
🟡 本週處理：
  1. {具體問題}
🟢 下次 /self-improve 時整理：
  1. {具體問題}

━━━ 健康度評分 ━━━
結構完整度：{N}% ████████░░
格式合規性：{N}% ██████████
項目時效性：{N}% ███████░░░
知識庫飽和度：{N}% ████░░░░░░

整體健康度：{N}%
```

## 快速修復建議（Claude 主動提供）

| 問題 | 快速修復 |
|------|----------|
| REQ 缺少驗收條件 | 「要我根據需求描述幫你補上驗收條件嗎？」 |
| ADR 缺少後果 section | 「要我根據現有內容推斷後果並補充嗎？」 |
| PENDING 超過 60 天 | 「要我整理成可以直接寄給甲方的 email 嗎？」 |
| PAT 缺少 tags | 「要我根據模式內容自動推薦 tags 嗎？」 |

append 記錄至 `wiki/log.md`。

---

## Wiki 層健康度（若 wiki/ 資料夾存在內容）

### 孤兒頁面掃描

掃描 `wiki/concepts/`、`wiki/entities/`、`wiki/sources/`、`wiki/questions/` 下所有 `.md`：
找出沒有任何其他頁面 `[[wikilink]]` 指向它的頁面。

```
🔗 孤兒頁面（{N} 個，無人連結）：
  wiki/entities/SomeService.md — 建議：從相關 project 或 knowledge/ 加連結
```

### 死連結掃描

掃描所有 wiki 頁面中的 `[[頁面名稱]]` 連結，確認目標檔案存在。

```
💀 死連結（{N} 個）：
  wiki/sources/SomeArticle.md → [[不存在的頁面]] — 建議：建立 stub 或移除連結
```

### 未解決矛盾掃描

掃描所有 wiki 頁面中的 `[!contradiction]` callout，列出待解決的矛盾。

```
⚡ 未解決矛盾（{N} 個）：
  wiki/entities/Redis.md + wiki/sources/SomeArticle.md — 發現日期：{YYYY-MM-DD}
```

### Dataview Dashboard（可選輸出）

若使用者說 `--dashboard`，輸出此 markdown 區塊可貼入 `wiki/meta/dashboard.md`：

````markdown
## Wiki 最近活動
```dataview
TABLE type, status, updated FROM "wiki" SORT updated DESC LIMIT 15
```

## 待孵化頁面（seed 狀態）
```dataview
LIST FROM "wiki" WHERE status = "seed" SORT updated ASC
```

## 未解決矛盾
```dataview
LIST FROM "wiki" WHERE contains(file.content, "[!contradiction]")
```
````
