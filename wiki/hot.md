---
type: hot-cache
updated: 2026-06-23
---

# 熱快取 — 最近工作脈絡

---

## 🔄 最近工作（2026-06-23）

**活躍專案**：知識庫系統本身（端對端驗證完成）
**上次工作**：2026-06-23

---

### 本次完成

**重大架構升級：整合 claude-obsidian wiki 知識層**

將系統從「純工程專案管理」升級為「工程層 + Obsidian 二腦」雙層架構。

**新增文件：**
- `hooks/hooks.json` — SessionStart/PostCompact/PostToolUse/Stop 四個 session 自動化 hooks
- `.claude/protocols/wiki-layer.md` — Obsidian wiki 層完整協議（frontmatter/wikilinks/callouts/資料夾界線）
- `wiki/concepts/_index.md` — 概念知識索引
- `wiki/entities/_index.md` — 實體/工具/服務知識索引
- `wiki/sources/_index.md` — 閱讀資料摘要索引
- `wiki/questions/_index.md` — 問答歸檔索引（複利增長機制）
- `wiki/overview.md` — 知識庫總覽
- `.raw/.gitkeep` — 不可修改原始文件存放區
- `knowledge/_schemas/callouts.md` — contradiction/gap/key-insight/stale 四種 callout 定義
- `.obsidian/snippets/vault-colors.css` — 資料夾色彩 + callout 視覺配置
- `.claude/commands/_ingest/input-url.md` — URL 輸入 → .raw/ 保存 → 標準解析流程

**修改文件：**
- `CLAUDE.md` — 加入知識路由邏輯、wiki 層結構說明、quick/standard/deep 查詢快捷
- `_ingest/detect.md` — 加入 ⑥ URL 偵測路由 + delta 檢查說明
- `_ingest/write.md` — 加入矛盾偵測（[!contradiction] callout）+ .manifest.json 更新
- `_query/lookup.md` — 完全重寫：quick/standard/deep 三段深度模式 + questions 歸檔機制
- `_health-check/structure.md` — 加入 wiki 層結構驗證清單
- `_health-check/report.md` — 加入孤兒頁面/死連結/未解決矛盾掃描 + Dataview dashboard 輸出
- `wiki/index.md` — 加入 wiki 知識層導航 + 頁面目錄區塊

### 重要整合決策

**取自 claude-obsidian：**
- Session hooks（SessionStart 自動讀 hot.md，Stop 提示更新）
- Wiki 知識層結構（concepts/entities/sources/questions）
- Obsidian callout 類型（contradiction/gap/key-insight/stale）
- URL 輸入 + .raw/ 原始文件架構
- /query 三段深度模式（quick/standard/deep）
- questions/ 歸檔機制（好答案複利增長）
- wiki-lint → 整合進 /health-check（孤兒/死連結/矛盾）

**不採用（評估後排除）：**
- DragonScale address counter（過度複雜，無必要）
- Semantic tiling（需要 ollama，環境依賴過重）
- /canvas（視覺功能，未來可選加）
- 社群宣傳 footer（不相關）

### 注意事項（下次繼續時記住）

- hooks/hooks.json 需要 Claude Code 設定中啟用 hooks 功能才生效
- .obsidian/snippets/vault-colors.css 需在 Obsidian 設定 → Appearance → CSS snippets 中啟用
- .raw/ 下的原始文件**不可修改**，只有 .raw/.manifest.json 可由 /ingest 更新
- wiki/questions/ 的歸檔是被動機制（/query 回答後主動詢問），不會自動觸發

### 最新新增（2026-06-23）

- `wiki/playbook.md` — 10 大高頻場景使用手冊（觸發情境/調用輸入/產出結果）
  - 10 個場景於 eshop-sunrise 虛擬測試專案全部驗證通過
  - 已登記至 wiki/index.md 快速導航

### 待辦（下次繼續）

- [ ] 啟用真實專案（`/project-init`）
- [ ] hooks/hooks.json 需在 Claude Code 設定中啟用
- [ ] vault-colors.css 需在 Obsidian → Appearance → CSS Snippets 中啟用
