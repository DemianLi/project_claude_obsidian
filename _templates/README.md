# _templates/ — 骨架檔案中心

> 這個目錄是所有**專案骨架檔案**（`/project-init` 建立、或建立新模組/元件/群組/ADR 時套用）的唯一來源。

---

## 與 knowledge/_schemas/ 的分工

- `_templates/` — 檔案**骨架**：一份檔案長什麼樣子、放在哪個路徑（例如 `00-overview.md`、`functional/README.md`、`_pending/_index.md`、`ADR-000-template.md`）
- `knowledge/_schemas/` — 條目**格式**：單一條目寫入時的欄位規則（例如一條 REQ、一條 PAT、一條 ADR 該有哪些必填欄位）

兩者互補：`_templates/project/04-decisions/ADR-000-template.md` 是「建立新 ADR 要複製的那個檔案」，其欄位定義則指向 `knowledge/_schemas/adr.md`「唯一格式參考」。修改欄位規則去 `_schemas/`，修改骨架長相或路徑去這裡。

---

## 目錄

| 路徑 | 用途 | 使用它的指令 |
|------|------|-------------|
| `project/` | `/project-init` 建立新專案時套用的完整骨架樹 | `/project-init` |
| `project/01-requirements/functional/README.md`「模組檔案結構」 | 新建 `functional/{module}.md` 時的骨架 | `/ingest`、`/migrate-kb --target=reqs` |
| `project/02-architecture/system-design/README.md`「元件檔案結構」 | 新建 `system-design/{component}.md` 時的骨架 | `/migrate-kb --target=arch` |
| `project/02-architecture/api-contracts/README.md`「群組檔案結構」 | 新建 `api-contracts/{group}.md` 時的骨架 | `/migrate-kb --target=api` |
| `project/04-decisions/ADR-000-template.md` | 新建 ADR 時複製 | `/save`、BEFORE CODING 步驟 6 |
| `project/02-architecture/_legacy-analysis.md` | 擴充案首次逆向工程時，若檔案不存在則依此建立 | `/reverse-engineer` |
| `dev-session.md` | 新建 dev-notes 時套用 | `/save`（`_save/gather.md`） |

## 使用規則

1. **套用前查閱**：任何指令在建立新骨架檔案前，先讀取對應模板，確認格式與路徑
2. **修改骨架**：只在這個目錄修改，指令文件中不重複內嵌骨架內容
3. `project/` 底下的檔案含 `{project_name}`、`{YYYY-MM-DD}` 等佔位符，套用時由 Claude 依實際專案資訊替換
