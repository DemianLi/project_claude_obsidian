# Phase 3：架構元件化（--target=arch）/ API 群組化（--target=api）

---

## --target=arch：架構元件化

使用者確認元件分組後執行：

1. 建立 `system-design/README.md`（說明元件分檔結構）
2. 對每個元件，建立 `system-design/{slug}.md`，含 Quick Context 頭
3. 更新 `arch-index.md` 的元件地圖（取代原來的 §段落）
4. 在原 `system-design.md` 頂部加遷移說明：
   ```markdown
   > ⚠️ 此文件已遷移至 system-design/ 目錄
   > 請見 arch-index.md 取得最新元件清單
   ```

---

## --target=api：API 群組化

使用者確認群組分組後執行：

1. 建立 `api-contracts/README.md`（說明群組結構）
2. 建立 `api-contracts/index.md`（薄索引，列出群組目錄）
3. 對每個群組，建立 `api-contracts/{module}.md`，含端點快速查詢表：
   ```markdown
   ## 端點快速查詢
   | Method | 路徑 | 說明 |
   |--------|------|------|
   | GET | /api/{路徑} | {功能} |
   ```
4. **驗證端點數量核對**：遷移前後總數必須一致
   - 若有差異 → **停止**，列出遺漏項目請使用者確認分配
5. 在原 `api-contracts.md` 頂部加遷移說明

→ 完成後讀取 `_migrate-kb/done.md`
