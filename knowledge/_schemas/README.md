# knowledge/_schemas/ — 格式定義中心

> 這個目錄是所有知識庫條目格式的**唯一真實來源**。
>
> 當任何指令需要寫入或驗證格式時，應先讀取對應的 schema 文件，
> 而不是在指令文件本身定義格式（避免格式定義散落各處）。

---

## 可用 Schema

| 檔案 | 對應的條目類型 | 使用它的指令 |
|------|--------------|-------------|
| `req.md` | REQ（功能需求） | `/ingest`, `/health-check`, `/reconcile` |
| `pat.md` | PAT（設計模式） | `/self-improve`, `/save`, BEFORE CODING 步驟 7 |
| `lesson.md` | LESSON（教訓） | `/self-improve`, `/save`, BEFORE CODING 步驟 7 |
| `adr.md` | ADR（架構決策） | `/save`, BEFORE CODING 步驟 6 |

---

## 使用規則

1. **寫入前查閱**：任何指令在建立新條目前，先讀取對應 schema，確認格式
2. **驗證時引用**：`/health-check` 以 schema 的「健康檢查規則」為驗證標準
3. **格式有疑問時**：以 schema 為準，不以各自指令文件中的範例為準
4. **修改格式**：只在這個目錄的 schema 文件修改，指令文件中的「格式範例」自動以此為準

---

## 版本說明

所有 schema 目前為 v1.0。若未來格式需要變更，在 schema 文件的 frontmatter 中更新 `version`，
並在文件末尾加入「版本變更記錄」section，說明從哪個版本改了什麼。
