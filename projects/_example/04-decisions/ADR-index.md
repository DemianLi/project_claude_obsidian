---
type: adr-index
project: _example
updated: {YYYY-MM-DD}
---

# 架構決策索引（ADR Index）

<!-- ⚡ Claude 讀取規則：
  1. 讀此索引 → 用「影響模組」欄位過濾當前任務相關的 ADR
  2. 只讀相關的 ADR-{ID}.md，不讀全部
  3. 若無相關 ADR → 跳過 04-decisions/ 目錄
-->

---

## 決策一覽

| ADR-ID | 標題 | 狀態 | 影響模組 | 關鍵決策（一句話） | 決策日期 |
|--------|------|------|---------|-----------------|---------|
| ADR-001 | {例：選用 JWT 認證} | accepted | auth | 使用 JWT+Refresh Token，不用 Session | {YYYY-MM-DD} |
| ADR-002 | {例：資料庫選型} | accepted | 全域 | 使用 PostgreSQL，放棄 MySQL（甲方現有環境） | {YYYY-MM-DD} |
| ADR-003 | {例：前端框架} | deprecated | ui | ~~Vue 2~~ → 已由 ADR-007 取代 | {YYYY-MM-DD} |

<!-- 新增 ADR 時，在此表格追加一行，同時建立 ADR-{NNN}.md 檔案 -->

---

## 狀態說明

| 狀態 | 含義 | Claude 的行為 |
|------|------|--------------|
| `accepted` | 現行決策，必須遵守 | 實作前確認不違反 |
| `proposed` | 討論中，尚未定案 | 提醒使用者此決策未完成 |
| `deprecated` | 已廢棄，不再適用 | 忽略，查看取代的 ADR |
| `superseded` | 已被取代，見 `superseded_by` | 讀取取代版本 |

---

## 快速過濾規則（Claude 使用）

```
若任務涉及「登入/認證/Token/Session」→ 看 auth 欄位的 ADR
若任務涉及「資料庫/查詢/資料結構」→ 看「全域」和相關模組的 ADR
若任務涉及「UI/前端/頁面」→ 看 ui 欄位的 ADR
若任務涉及「API/外部整合」→ 看 api/integration 欄位的 ADR
若無匹配 → 跳過讀取個別 ADR 檔案
```

---

## ADR 檔案清單

```
04-decisions/
├── ADR-index.md         ← 你在這裡（永遠先讀）
├── ADR-000-template.md  ← 建立新 ADR 時複製此模板
├── ADR-001-{標題}.md
├── ADR-002-{標題}.md
└── ...
```
