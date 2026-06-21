# functional/ — 需求模組目錄

此目錄存放各模組的詳細需求，是 `functional-index.md` 的深層內容層。

## 讀取規則

Claude 不直接讀取此目錄，**必須先讀 `../functional-index.md`** 找到相關模組後才讀取對應檔案。

## 模組檔案命名

每個模組一個 `.md` 檔案，命名使用英文 slug：

```
functional/
├── auth.md          # 認證與授權
├── order.md         # 訂單管理
├── inventory.md     # 庫存管理
├── report.md        # 報表與匯出
├── notification.md  # 通知系統
└── ...
```

## 模組檔案結構（每個模組檔案的格式）

```markdown
---
type: functional-module
module: {模組名}
project: {專案名}
updated: {YYYY-MM-DD}
---

# {模組中文名} 需求

## 📌 Quick Context
<!-- ⚡ Claude Stage A：先讀此區塊，確認本模組是否與當前任務相關 -->
**已確認需求**：{N} 條 ｜ **待確認**：{N} 條 ｜ **廢棄**：{N} 條
**熱點需求**（最近變更/阻塞中）：{REQ-FXXX 標題}、{REQ-FXXX 標題}
**最後變更**：{REQ-FXXX} — {一句話摘要}（{YYYY-MM-DD}）
<!-- /Quick Context Stage A End -->

---

## ⚡ REQ 快速掃描表（第三層索引）

<!-- ⚡ Claude Stage B：讀此表找到相關 REQ-ID，再只讀對應的詳細條目 -->
<!-- /save 和 /ingest 自動維護此表，不要手動大幅修改 -->

| REQ-ID | 標題（一句話） | 狀態 | 關鍵字 |
|--------|-------------|------|--------|
| REQ-F001 | {例：email+密碼登入} | ✅ | 登入, email, 密碼 |
| REQ-F002 | {例：密碼最少 8 碼含大小寫} | ✅ | 密碼, 強度, 規則 |
| REQ-F003 | {例：忘記密碼寄 email 重設} | 🕐 | 忘記密碼, email, 重設 |

<!-- Stage B 讀取指引：
  → 比對當前任務關鍵字 vs 上表「關鍵字」欄位
  → 找到相關 REQ-ID 後，跳至下方對應的詳細條目
  → 無交集 → 此模組與當前任務無關，停止讀取
-->

---

## 需求詳細條目

### REQ-F{XXX}：{需求標題}

| 欄位 | 內容 |
|------|------|
| **狀態** | ✅ 已確認甲方 |
| **確認日期** | {YYYY-MM-DD} |
| **來源文件** | {文件名} |
| **合約版本** | v{N.N} |

**描述**：{需求描述}

**驗收條件**：
- [ ] {條件一}
- [ ] {條件二}
```

## 三層讀取路徑說明

```
Stage 0：functional-index.md（模組目錄）
  ↓ 識別相關模組
Stage A：functional/{module}.md 的 Quick Context
  ↓ 確認模組相關，且了解整體狀態
Stage B：functional/{module}.md 的 REQ 快速掃描表
  ↓ 比對關鍵字，識別具體的相關 REQ-ID
Stage C：functional/{module}.md 中的對應詳細條目
  ↓ 只讀相關 REQ 的完整描述與驗收條件
```

這三層確保即使單一模組有 200+ 條需求，Claude 也只讀取真正相關的 1–5 條。

## 為何拆分模組

- 單一 functional.md 累積至 1000+ 條需求時，Claude 讀取整份文件是嚴重的 token 浪費
- 模組化後，一個 50 條需求的模組檔案只有全量的 5%
- 加上 Quick Context header，Claude 甚至可以在不讀完整模組的情況下判斷相關性
