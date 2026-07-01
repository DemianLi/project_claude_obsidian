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

套用 `{KB_ROOT}/_templates/project/` 底下的骨架，在 `projects/{專案名稱}/` 下依相同相對路徑建立每一份檔案，並將 `{project_name}`、`{YYYY-MM-DD}` 等佔位符換成本次收集的實際資訊：

```
00-overview.md
01-requirements/functional-index.md ｜ functional/README.md ｜ non-functional.md ｜ scope.md
01-requirements/_pending/_index.md ｜ _inferred/_index.md
02-architecture/arch-index.md ｜ system-design/README.md ｜ api-contracts/index.md ｜ api-contracts/README.md
03-client-context/stakeholders.md ｜ existing-system.md ｜ domain-knowledge.md
04-decisions/ADR-index.md ｜ ADR-000-template.md
05-dev-notes/_index.md
06-qa-testing/bugs-active.md（bugs/ 資料夾留空，各 BUG 建立時各自一檔）
CHANGELOG.md
```

`scope.md` 依 BEFORE CODING Stage 1 / `/cr` 的依賴需求填入初始合約版本。骨架的完整定義（含各檔案為何長這樣）見 `_templates/README.md`。

**collab/ 建立方式**（詢問後依人數建立）：

詢問：「這個專案有多位工程師協作嗎？請提供成員縮寫列表（例如：DL, MC, YJ）」

每位工程師依 `_templates/project/collab-entry.md` 建立 `collab/{initials}.md`（有效類型值見 `knowledge/_schemas/collab.md`）。

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

套用 `_templates/project/code-root-CLAUDE.md`，將佔位符換成實際資訊後，在 `{CODE_ROOT}/CLAUDE.md` 建立。

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
