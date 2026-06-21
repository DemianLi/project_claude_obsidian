---
type: operation-log
---

# 操作日誌

> Append-only 紀錄。每次 `/save` 由 Claude 新增一筆，不得修改或刪除舊紀錄。

## 格式
```
### [YYYY-MM-DD] 專案名稱 — 操作摘要
- 做了什麼
- 重要決策
- 遺留問題
```

---

### [2026-06-21] 系統初始化 — 知識庫建立
- 初始化軟體工程知識庫系統
- 建立完整資料夾結構（projects、knowledge、wiki、_templates、.claude/commands）
- 建立 CLAUDE.md 協作指引
- 建立五個 Claude Code slash commands（project-init、ingest、query、save、self-improve）
- 系統就緒，等待第一個專案

### [2026-06-21] 系統深化 — 完整設計迭代
- **ingest 三階段確認閘**：解析/確認/寫入分離，模糊需求存 `_pending.md`（同專案內），不污染 `functional.md`
- **無主文件分流**：新增 `_inbox/_unassigned/` 處理不確定歸屬的文件
- **背景知識三層分類**：新增 `domain-knowledge.md`，`/ingest` 加背景知識路由（stakeholders / existing-system / domain-knowledge）
- **BEFORE CODING 強化**：加入讀取 `03-client-context/` 步驟，確保實作前了解甲方環境限制與領域術語
- **/save 加背景知識更新提醒**：對話中學到的甲方背景也會被捕捉
- **/research 指令**：知識庫約束輪廓注入網路搜索，結果做相容性驗證排名
- **/query --verify 模式**：Claude 用自己的話重述理解（非引用原文），請使用者確認或糾正
- **逆向工程三層分離**：新增 `/reverse-engineer` 指令、`_inferred.md`（推測+缺口）、`_legacy-analysis.md`（結構事實）
- **BEFORE CODING 停止格式**：遇到 INF/GAP 展開完整細節與問甲方問題，不只報 ID
- **對帳機制**：`/ingest` 加語意對帳步驟；新增 `/reconcile` 指令做全面語意掃描與清理
- **重複資訊衝突處理規則**：定義優先序（functional > _pending > _inferred），發現重複不靜默
- **風險分配原則**：寫入 CLAUDE.md 作為系統核心設計哲學，Claude 提供選項，使用者做決策
