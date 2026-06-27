# Phase 2：需求模組化（--target=reqs）

使用者確認分組方案後執行：

## Step 1：建立 functional/ 目錄結構

建立 `01-requirements/functional/README.md`（說明模組分檔結構）

## Step 2：對每個確認的模組，建立 functional/{module}.md

```markdown
---
type: functional-module
module: {模組名}
project: {專案名}
updated: {YYYY-MM-DD}
---

# {模組中文名} 需求

## 📌 Quick Context
| 欄位 | 內容 |
|------|------|
| **已確認需求** | {N} 條 |
| **待確認需求** | {N} 條 |
| **熱點需求** | {最近更新的 REQ} |
| **最後變更** | {最近變更的 REQ 和日期} |

---

## REQ 快速掃描表
| REQ-ID | 標題一句話 | 狀態 | 關鍵字 |
|--------|-----------|------|-------|
| REQ-F001 | {標題} | ✅ | {關鍵字} |

---

{從 functional.md 搬移的對應需求條目}
```

## Step 3：建立 functional-index.md（薄索引）

填入模組目錄和快速定位規則，讓 BEFORE CODING 可精準路由。

→ 完成後讀取 `_migrate-kb/done.md`
