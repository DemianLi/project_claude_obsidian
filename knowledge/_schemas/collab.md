---
type: schema
entity: COLLAB
version: 1.0
updated: 2026-06-28
---

# Schema：COLLAB（工程師鎖定狀態）

> 這是所有指令的唯一格式參考。
> `/project-init` 建立時、`/save`（`_collab/update.md`）寫入時、`_collab/check.md` 讀取比對時、`/health-check` 驗證時，均以此為準。
> 權威範例見 `.claude/commands/project-init.md` collab/ 建立方式 section。

---

## 完整格式

```markdown
---
engineer: {initials}
name: {姓名}
role: {角色}
updated: {YYYY-MM-DD}
---

# 鎖定狀態 — {initials}

| 類型 | 鎖定項目 | 位置 | 鎖定日期 | 備注 |
|------|---------|------|---------|------|
| {類型} | {項目} | {位置} | {YYYY-MM-DD} | {note} |
```

無鎖定項目時，表格保留一行佔位：`| （無） | — | — | — | — |`

---

## 必填欄位

| 欄位 | 必填 | 說明 |
|------|------|------|
| frontmatter `engineer` | ✅ | 工程師縮寫，與檔名一致 |
| frontmatter `updated` | ✅ | YYYY-MM-DD 格式，每次 `/save` 更新鎖定狀態時同步更新 |
| `active_work` 表格每列「類型」 | ✅（若有鎖定列） | 見下方有效值；佔位列 `| （無） | — | — | — | — |` 不算鎖定列，不受此規則檢查 |
| `active_work` 表格每列「鎖定日期」 | ✅（若有鎖定列） | YYYY-MM-DD 格式；佔位列同上不檢查 |
| frontmatter `name` / `role` | ⬜ 選填 | |

---

## 有效類型值

| 類型 | 對應檔案 |
|------|---------|
| `REQ` | `functional/{module}.md` 的具體 REQ ID |
| `元件` | `02-architecture/system-design/{component}.md` |
| `API群組` | `02-architecture/api-contracts/{group}.md` |

---

## 備注欄填寫規則

超過 14 天未更新的鎖定，「備注」欄填「⏰ 已 {N} 天未更新，可能已過期」；14 天以內留空。此規則由 `_collab/check.md` Step 3-4 在 BEFORE CODING 比對時計算，僅供提示，不代表系統會自動刪除該鎖定（見 `wiki/collab-protocol.md` 二）。

---

## 健康檢查規則（供 /health-check 使用）

一份 `collab/{initials}.md` 被視為「不健康」如果：
- 缺少 frontmatter `engineer` 或 `updated` 欄位
- `active_work` 表格中「類型」值不在有效列表中
- 鎖定日期格式不是 YYYY-MM-DD
- frontmatter 的 `engineer` 與檔名不一致
