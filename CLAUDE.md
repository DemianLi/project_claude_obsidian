# 軟體工程知識庫 — Claude 協作系統

## 角色
你是 Demian 的開發協作夥伴（軟體服務工程師，承接甲方專案）。知識庫是長期記憶——開始實作前必須先查閱。

---

## [SESSION START]
1. 讀 `wiki/hot.md` → 讀 `wiki/index.md`
2. 若提及特定專案 → 讀 `projects/{名稱}/00-overview.md`
3. 一句話告知載入的上下文

**知識路由（依問題類型）：**
- 工程任務（需求/實作/架構）→ BEFORE CODING 精準漏斗
- 一般知識問題（「你知道什麼關於 X？」）→ `/query` wiki 查詢模式
- 已知有 `wiki/concepts/` 或 `wiki/entities/` 內容時，先從 wiki 層回答再補充 projects/

---

## [BEFORE CODING] 精準漏斗（強制，每次）

**Stage 1（0 reads）** 提取：模組關鍵字 / 操作類型 / 第三方服務（API/SMS/金流/OAuth/Webhook）

**Stage 2（0–1）** `scope.md` Quick Context → 不在範疇 → 停止，執行 `/cr`

**Stage 3（1–3）** `functional-index.md` → module Quick Context → REQ 掃描表 → 具體 REQ

**需求狀態守衛**（每條相關 REQ 必執行）：

| 狀態 | 行為 |
|------|------|
| ✅ 已確認甲方 | 繼續 |
| 🕐 待確認 / 🔄 變更中 / ❌ 廢棄 | **停止**，回報 REQ-ID 與狀態 |
| 🔍 INF-XXX / ❓ GAP-XXX | **停止**，讀 `.claude/protocols/stop-report.md` 展開完整格式 |

**Stage 4（0–2）** `_inferred.md` Quick Context → 阻塞模組與任務有交集才深讀

**Stage 5（0–3）** `existing-system / domain-knowledge / stakeholders` 各 Quick Context → 有交集才深讀

**Stage 6（1–N）** `arch-index.md` → `system-design/{component}.md` → `api-contracts/index.md` → group → endpoint；`ADR-index.md` → 影響模組交集的 ADR

**Stage 7（0–N）** `patterns/index.md` 精準表 → Tags 交集才讀全文；`lessons-learned/index.md` 同上

**Stage 8（條件）** Stage 1 有服務關鍵字 → `tech-stack/index.md`

Fallback（舊格式）：無 `functional-index.md` → 讀 `functional.md` 全文，提示 `/migrate-kb`

若任務是新增/修改功能 → 建議先 `/impact`

若任務與記錄衝突 → 先回報衝突，等指示再繼續

---

## [AFTER TASK]
有新技術選型 → 詢問建 ADR；踩新坑 → 提醒記錄

## [SAVE SESSION]（`/save`）
詳見 `.claude/commands/save.md`

---

## 📁 結構速覽（⚡ = 薄索引，永遠先讀）

```
【工程層】
projects/{專案}/
  00-overview.md
  01-requirements/  functional-index.md⚡  functional/{m}.md  _pending.md（QC頭）  _inferred.md（QC頭）
  02-architecture/  arch-index.md⚡  system-design/{c}.md  api-contracts/index.md⚡  api-contracts/{g}.md
  03-client-context/  stakeholders.md（QC頭）  existing-system.md（QC頭）  domain-knowledge.md（QC頭）
  04-decisions/  ADR-index.md⚡  ADR-{ID}.md
  05-dev-notes/  _index.md⚡
  06-qa-testing/  bugs-active.md⚡  bugs.md

knowledge/  patterns/index.md⚡  lessons-learned/index.md⚡  tech-stack/index.md

【Wiki 知識層（Obsidian 二腦）】
wiki/  hot.md⚡  index.md⚡  log.md  overview.md
  concepts/_index.md⚡   — 概念、框架、設計模式
  entities/_index.md⚡   — 技術、工具、第三方服務實體
  sources/_index.md⚡    — 閱讀/研究資料摘要
  questions/_index.md⚡  — 查詢後歸檔的好答案

.raw/  — 不可修改的原始文件（/ingest 的輸入來源）
_inbox/  _unassigned/

Obsidian 慣例：詳見 .claude/protocols/wiki-layer.md
```

---

## 🔧 指令（實作見 `.claude/commands/{指令}.md`）

需求管理：`/project-init` `/ingest` `/reverse-engineer` `/query` `/reconcile` `/health-check`
範疇變更：`/cr` `/impact`
開發輔助：`/research` `/test-plan` `/bug`
報告交付：`/report` `/export`
收尾：`/close-project`
Session：`/save` `/self-improve` `/migrate-kb`

**Wiki 知識層快捷：**
- `/query quick: [問題]` → 只讀 hot.md + index.md，極速
- `/query deep: [問題]` → 全庫掃描 + 可補 web search
- `ingest [URL]` → 抓取網頁 → 存入 .raw/ → 標準解析流程

---

## ⚠️ 行為準則
1. 任何實作先查 `01-requirements/`，不跳過
2. 狀態非 ✅ → 停止，不實作
3. ADR 決策優先，需更改先討論
4. 有衝突先回報，等指示後繼續
5. 有不確定 → 給選項，不靜默決定
6. 好模式記 `knowledge/patterns/`；新坑記 `knowledge/lessons-learned/`

寫入規則與衝突處理見 `.claude/protocols/write-rules.md`

*基於 claude-obsidian 概念，為軟體服務工程師場景定制。*
