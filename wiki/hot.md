---
type: hot-cache
updated: 2026-06-21
---

# 熱快取 — 最近工作脈絡

---

## 🔄 最近工作（2026-06-21）

**活躍專案**：知識庫系統本身（初始化建置）  
**上次工作**：2026-06-21（系統建置日）

---

### 本次完成

今日完整建立「軟體工程知識庫 — Claude 協作系統」，從零到完整可用。

**建立的指令（`.claude/commands/`）：**

| 指令 | 核心功能 |
|------|----------|
| `/project-init` | 建立新專案完整資料夾結構 |
| `/ingest` | 三階段確認閘解析甲方文件（解析→確認→寫入） |
| `/reverse-engineer` | 逆向分析程式碼/DB，區分事實/推測/缺口三層 |
| `/query` | 查詢知識庫；`--verify` 模式驗證 Claude 理解 |
| `/research` | 知識庫約束注入網路搜索，驗證解方相容性 |
| `/reconcile` | 語意比對清理重複與已解決的待釐清項目 |
| `/save` | 儲存 session，更新熱快取與背景知識 |
| `/self-improve` | 提煉 dev-notes 至 patterns 與 lessons-learned |

**建立的知識庫結構：**
- `projects/{專案}/` — 7 層子資料夾（需求、架構、甲方背景、決策、筆記、測試）
- `projects/{專案}/01-requirements/` — `functional.md`、`_pending.md`、`_inferred.md`
- `projects/{專案}/02-architecture/` — 加入 `_legacy-analysis.md`
- `projects/{專案}/03-client-context/` — `stakeholders`、`existing-system`、`domain-knowledge`
- `knowledge/` — `patterns`、`tech-stack`、`lessons-learned`
- `_inbox/_unassigned/` — 無主文件暫存區

---

### 重要設計決策

**決策一：解析與寫入分離**
`/ingest` 採三階段——Phase 1 只讀，Phase 2 人工確認，Phase 3 才寫入。
模糊需求不進 `functional.md`，只存 `_pending.md`（同專案內）。

**決策二：三層知識分類**
結構性事實 → `_legacy-analysis.md`
推測業務邏輯 → `_inferred.md`（🔍 信心度標記）
邏輯缺口 → `_inferred.md`（❓ 缺口區）
三者嚴格隔離，不得混入 `functional.md`。

**決策三：風險分配原則**
Claude 整理資訊、識別問題、提供選項；使用者做所有業務決策。
有任何不確定就給選項，不靜默決定。這個原則寫入 CLAUDE.md 讓所有使用者繼承。

**決策四：語意對帳而非關鍵字匹配**
`/reconcile` 和 `/ingest` 的對帳步驟用語意比對，
防止「登入要安全」和「密碼最少 8 碼」因關鍵字不同而被視為無關。

**決策五：知識庫驅動的網路搜索**
`/research` 先讀 `existing-system.md`、`domain-knowledge.md`、`non-functional.md`，
帶著約束輪廓搜索，結果回頭驗證相容性。

---

### 檔案分流設計

```
甲方文件
├── 知道是哪個專案
│   ├── 需求明確   → functional.md（✅ 確認後）
│   ├── 需求模糊   → _pending.md（🕐 同專案內）
│   └── 逆向分析   → _legacy-analysis.md + _inferred.md
└── 不知道是哪個專案
    └── _inbox/_unassigned/（確認後 /ingest 重新處理）
```

---

### 注意事項（下次繼續時記住）

- `_inferred.md` 的推測升格唯一路徑：甲方回覆 → `/ingest [回覆]` → 走確認流程 → `functional.md`
- Claude 停止時的標準格式：展開完整 INF/GAP 細節 + 建議問甲方的文字 + 提議整理成 email
- 發現 `functional.md` 有確認版但 `_pending.md` 還有舊版時：不靜默，一律回報
- 優先序：`functional.md` > `_pending.md` > `_inferred.md`

---

### 待辦（下次繼續）

- [ ] 建立第一個真實專案（`/project-init`）
- [ ] 測試 `/ingest` 流程（帶入真實甲方文件驗證）
- [ ] 考慮是否需要 Obsidian Local REST API 啟用 MCP 直接讀寫
