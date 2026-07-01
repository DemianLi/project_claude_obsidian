# Phase 3：架構元件化（--target=arch）/ API 群組化（--target=api）

---

## --target=arch：架構元件化

使用者確認元件分組後執行：

1. 依 `_templates/project/02-architecture/system-design/README.md` 建立同名 README.md（說明元件分檔結構）
2. 對每個元件，依該 README「元件檔案結構」建立 `system-design/{slug}.md`
3. 依 `_templates/project/02-architecture/arch-index.md` 更新 `arch-index.md` 的元件地圖（取代原來的 §段落）
4. 在原 `system-design.md` 頂部加遷移說明：
   ```markdown
   > ⚠️ 此文件已遷移至 system-design/ 目錄
   > 請見 arch-index.md 取得最新元件清單
   ```

---

## --target=api：API 群組化

使用者確認群組分組後執行：

1. 依 `_templates/project/02-architecture/api-contracts/README.md` 建立同名 README.md（說明群組結構）
2. 依 `_templates/project/02-architecture/api-contracts/index.md` 建立 `api-contracts/index.md`（薄索引，列出群組目錄）
3. 對每個群組，依該 README「群組檔案結構」建立 `api-contracts/{module}.md`
4. **驗證端點數量核對**：遷移前後總數必須一致
   - 若有差異 → **停止**，列出遺漏項目請使用者確認分配
5. 在原 `api-contracts.md` 頂部加遷移說明

→ 完成後讀取 `_migrate-kb/done.md`
