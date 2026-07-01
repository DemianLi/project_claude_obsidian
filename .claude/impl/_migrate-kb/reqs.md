# Phase 2：需求模組化（--target=reqs）

使用者確認分組方案後執行：

## Step 1：建立 functional/ 目錄結構

依 `_templates/project/01-requirements/functional/README.md` 建立同名 README.md（說明模組分檔結構）

## Step 2：對每個確認的模組，建立 functional/{module}.md

骨架依 `_templates/project/01-requirements/functional/README.md`「模組檔案結構」，將搬移的對應需求條目填入「需求詳細條目」區塊（單條 REQ 欄位格式依 `knowledge/_schemas/req.md`）。

## Step 3：建立 functional-index.md（薄索引）

骨架依 `_templates/project/01-requirements/functional-index.md`，填入模組目錄和快速定位規則，讓 BEFORE CODING 可精準路由。

→ 完成後讀取 `_migrate-kb/done.md`
