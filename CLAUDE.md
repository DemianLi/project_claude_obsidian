# 軟體工程知識庫 — Claude 協作系統

KB_ROOT=`~/Projects_vibecoding/claude_obsidien_setting`（知識庫，版控由 Obsidian git 插件自動管理）｜CODE_ROOT=`~/Projects_vibecoding/{project}`（程式碼，工程師自管）｜路徑除非標 `{CODE_ROOT}` 否則相對 KB_ROOT。結構總覽見 `.claude/protocols/structure-map.md`。

[SESSION START] 讀 `{KB_ROOT}/wiki/hot/*.md`→`wiki/index.md`（提及專案加讀 `projects/{名稱}/00-overview.md`；`.claude/collab/` 存在則顯示鎖定狀況）→一句話告知上下文。工程任務走下方漏斗；一般知識問題走 `/query`（wiki 層優先）。

[BEFORE CODING]（任何實作前強制執行，不可跳過，路徑皆相對 `{KB_ROOT}/projects/{名稱}/` 除非另標）
1. `scope.md` 不在範疇 → 停止，執行 `/cr`
2. `functional-index.md`→module→REQ：✅繼續｜🕐/🔄/❌→停止回報狀態｜🔍INF/❓GAP→讀 `{KB_ROOT}/.claude/protocols/stop-report.md` 展開
3.（若 `.claude/collab/` 存在）讀 `{KB_ROOT}/.claude/impl/_collab/check.md` 偵測鎖定衝突，有衝突要求確認才繼續
4. `_inferred/_index.md` 阻塞模組與任務交集才讀個別 `_inferred/{ID}.md`
5. `03-client-context/`、`02-architecture/`（`arch-index`→`system-design/`/`api-contracts/`）、`04-decisions/` ADR，交集才深讀
6.（依服務關鍵字）`{KB_ROOT}/knowledge/{patterns,lessons-learned,tech-stack}`，交集才讀
無 `functional-index.md` → 停止，先執行 `/migrate-kb`｜任務與記錄衝突 → 先回報，等指示再繼續

[AFTER TASK] 新技術選型→問建 ADR；踩坑→提醒記錄
[SAVE SESSION] `/save`，見 `{KB_ROOT}/.claude/commands/save.md`

行為準則：①查閱不跳過 ②ADR優先，改先討論 ③不確定給選項不靜默 ④好模式/坑記 `{KB_ROOT}/knowledge/` ⑤code 與 knowledge 不混放（寫入規則見 `{KB_ROOT}/.claude/protocols/write-rules.md`）
