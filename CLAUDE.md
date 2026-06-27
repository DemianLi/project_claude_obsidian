# 軟體工程知識庫 — Claude 協作系統

KB_ROOT=`~/Projects_vibecoding/claude_obsidien_setting`（知識庫，版控由 Obsidian git 插件自動管理）｜CODE_ROOT=程式碼實際所在目錄（工程師自管，父路徑不限，資料夾名對應 `projects/{名稱}/`）｜路徑除非標 `{CODE_ROOT}` 否則相對 KB_ROOT。結構總覽見 `.claude/protocols/structure-map.md`。

[SESSION START] 讀 `{KB_ROOT}/wiki/hot/*.md`→`wiki/index.md`（提及專案加讀 `projects/{名稱}/00-overview.md`；`collab/` 存在則顯示鎖定狀況）→一句話告知上下文。工程任務走下方漏斗；一般知識問題走 `/query`（wiki 層優先）。

[BEFORE CODING] 任何實作前強制執行，不可跳過，步驟見 `{KB_ROOT}/.claude/protocols/before-coding.md`

[AFTER TASK] 新技術選型→問建 ADR；踩坑→提醒記錄
[SAVE SESSION] `/save`，見 `{KB_ROOT}/.claude/commands/save.md`

行為準則：①查閱不跳過 ②ADR優先，改先討論 ③不確定給選項不靜默 ④好模式/坑記 `{KB_ROOT}/knowledge/` ⑤code 與 knowledge 不混放（寫入規則見 `{KB_ROOT}/.claude/protocols/write-rules.md`）
