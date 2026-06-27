# BEFORE CODING 閘門

> 任何實作前強制執行，不可跳過。路徑皆相對 `{KB_ROOT}/projects/{名稱}/` 除非另標。

1. `scope.md` 不在範疇 → 停止，執行 `/cr`
2. `functional-index.md`→module→REQ：✅繼續｜🕐/🔄/❌→停止回報狀態｜🔍INF/❓GAP→讀 `{KB_ROOT}/.claude/protocols/stop-report.md` 展開
3.（若 `collab/` 存在）讀 `{KB_ROOT}/.claude/impl/_collab/check.md` 偵測鎖定衝突，有衝突要求確認才繼續
4. `_inferred/_index.md` 阻塞模組與任務交集才讀個別 `_inferred/{ID}.md`
5. `03-client-context/`、`02-architecture/`（`arch-index`→`system-design/`/`api-contracts/`）、`04-decisions/` ADR，交集才深讀
6.（依服務關鍵字）`{KB_ROOT}/knowledge/{patterns,lessons-learned,tech-stack}`，交集才讀

無 `functional-index.md` → 停止，先執行 `/migrate-kb`｜任務與記錄衝突 → 先回報，等指示再繼續
