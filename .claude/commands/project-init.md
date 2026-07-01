---
description: 初始化新專案，建立完整知識庫結構與薄 CLAUDE.md
---
# /project-init — 建立新專案

## 觸發方式
```
/project-init [專案名稱]
```

## 執行步驟

收到此指令後，依序執行：

**1. 確認專案名稱**
若未提供名稱，詢問：「專案名稱是什麼？（建議用英文或拼音，例如：eshop-acme 或 erp-client-b）」

**2. 詢問基本資訊（一次問清楚）**
```
請提供以下資訊（有的填，沒有的留空）：
1. 甲方名稱：
2. 專案類型：新開發 / 系統擴充 / 維護
3. 預計時程：
4. 主要技術棧（若已知）：
5. 一句話描述這個專案要做什麼：
```

**3. 建立資料夾結構（含所有薄索引）**
在 `projects/{專案名稱}/` 下建立：

```
00-overview.md                    （填入收集的資訊）
01-requirements/
  functional-index.md             ← 薄索引 L1（模組目錄）
  functional/
    README.md                     ← 說明三層讀取結構（L1模組→L2模組Quick Context→L3 REQ掃描表）
  non-functional.md               （空白模板）
  scope.md                         （空白模板，BEFORE CODING Stage 1 / `/cr` 依賴此檔）
  _pending/
    _index.md                     ← 薄索引（含 QUICK CONTEXT 頭）；各 PENDING 各自一檔
  _inferred/
    _index.md                     ← 薄索引（含 QUICK CONTEXT 頭）；各 INF/GAP 各自一檔
02-architecture/
  arch-index.md                   ← 薄索引（元件地圖）
  system-design/
    README.md                     ← 說明元件分檔結構
  api-contracts/
    index.md                      ← 薄索引（端點群組目錄）
    README.md                     ← 說明端點群組結構
03-client-context/
  stakeholders.md                 （含 Quick Context 決策者摘要頭）
  existing-system.md              （含 Quick Context 關鍵限制頭）
  domain-knowledge.md             （含 Quick Context 關鍵字頭）
04-decisions/
  ADR-index.md                    ← 薄索引（空白模板）
  ADR-000-template.md             （建立新 ADR 時複製）
05-dev-notes/
  _index.md                       ← 薄索引（空白模板）
06-qa-testing/
  bugs-active.md                  ← 薄索引（空白模板）
  bugs/                           ← 各 BUG 各自一檔（BUG-001.md, BUG-002.md...）
CHANGELOG.md                      （初始版本）
collab/                           ← 各工程師各自一檔（DL.md, MC.md...），選配
```

**collab/ 建立方式**（詢問後依人數建立）：

詢問：「這個專案有多位工程師協作嗎？請提供成員縮寫列表（例如：DL, MC, YJ）」

每位工程師建立 `collab/{initials}.md`：
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
| （無） | — | — | — | — |
```
> 有效類型值與對應檔案見 `knowledge/_schemas/collab.md`「有效類型值」表

單人專案可跳過此步驟（collab/ 資料夾不存在時所有協作機制自動停用）。

各薄索引在建立時為空白模板；後續由 `/ingest`、`/bug`、`/save` 指令自動維護內容。若是「擴充案」（既有系統），特別提醒：
- `existing-system.md` 必填，越詳細越好
- 建議立即執行 `/reverse-engineer` 填充 `_inferred/_index.md`

**4. 更新 `{KB_ROOT}/wiki/index.md`**
將新專案加入「進行中的專案」表格。

**5. 更新 `{KB_ROOT}/wiki/hot/{engineer}.md`**
記錄新專案已建立，設為當前活躍專案。

**6. 建立程式碼倉庫的薄 CLAUDE.md**

詢問：「程式碼倉庫路徑？」（不假設特定上層目錄，直接請使用者提供完整路徑）

在 `{CODE_ROOT}/CLAUDE.md` 建立以下內容：

```markdown
# {project_name} — 開發工作區

## 路徑設定
KB_ROOT: {填入實際絕對路徑，不是文字描述——這份薄 CLAUDE.md 會放到 CODE_ROOT，與 KB_ROOT 通常不同目錄，寫死絕對路徑才能讓 CODE_ROOT 端找到 KB_ROOT}
CODE_ROOT: {使用者確認的路徑}
PROJECT_NAME: {project_name}

## 使用說明
完整系統規則（BEFORE CODING、/save、所有指令）在 KB_ROOT 的 CLAUDE.md。
SESSION START 時，先讀 `{KB_ROOT}/CLAUDE.md`，再讀 `{KB_ROOT}/wiki/hot/*.md`。

## 本專案知識庫路徑
需求 / 架構 / 決策：`{KB_ROOT}/projects/{project_name}/`
程式碼（此目錄）：`{CODE_ROOT}/`

## 版控說明
- 知識庫（KB_ROOT）→ Obsidian git 插件自動管理，無需手動操作
- 程式碼（CODE_ROOT，此目錄）→ 工程師自行 git 管理
```

若使用者未提供路徑，停下來請使用者補充（不靜默猜測路徑）；若路徑不存在則提醒需先建立目錄。多工程師團隊共用同一個 CODE_ROOT 時，這份薄 `CLAUDE.md` 會隨程式碼 repo 自動同步給全員；指令層（slash commands）的團隊共用設定見 `README.md`「團隊共用設定」。

**7. 完成回報**
```
✅ 專案 [{名稱}] 建立完成

📂 知識庫：{KB_ROOT}/projects/{名稱}/
📂 程式碼：{CODE_ROOT}/（薄 CLAUDE.md 已產生）
⚡ 薄索引已建立：functional-index / arch-index / ADR-index / dev-notes/_index / bugs-active
📋 下一步：
  1. 將甲方文件放入 {KB_ROOT}/_inbox/，執行 /ingest 自動解析並填充 functional-index
  2. 確認非功能需求：{KB_ROOT}/projects/{名稱}/01-requirements/non-functional.md
  3. 若為擴充案：填寫 existing-system.md，執行 /reverse-engineer
```
