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
