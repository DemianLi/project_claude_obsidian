---
type: schema
entity: TECH-STACK
version: 1.0
updated: 2026-07-01
---

# Schema：TECH-STACK（技術棧筆記）

> 這是所有指令的唯一格式參考。
> `/self-improve`（`_self-improve/patterns-tech.md`）寫入時、`/health-check`（`_health-check/knowledge.md`）驗證時、`/research`／`/query`／`/export`／`/save` 讀取比對時，均以此為準。
> 權威範例見 `knowledge/tech-stack/index.md` 與既有條目檔案（`aws.md`、`mysql.md` 等）。

---

## 索引格式（`knowledge/tech-stack/index.md`）

```markdown
| 項目 | 類型 | 檔案 | 關鍵字 | 使用次數 | 最後使用 | 完整度 |
|------|------|------|--------|---------|---------|--------|
| {服務名稱} | {類型 emoji + 分類} | [{slug}.md]({slug}.md) | {關鍵字, 逗號分隔} | {N} | {YYYY-MM-DD 或 —} | {⬜ 空白 / 🟡 部分 / ✅ 完整} |
```

新增技術時：在表格追加一行 + 建立對應 `{slug}.md`；`/self-improve` 時更新使用次數/最後使用。

---

## 有效分類值

| 分類 | Emoji | 條目格式 |
|------|-------|----------|
| 第三方服務 | 🔌 | 完整格式（見下） |
| 後端框架 | 🖥 | 精簡格式 |
| 資料庫 | 🗄 | 精簡格式 |
| 雲端/基礎設施 | ☁️ | 精簡格式 |
| 前端 | 🎨 | 精簡格式 |
| DevOps | 🔧 | 精簡格式 |

---

## 條目格式（`knowledge/tech-stack/{slug}.md`）

### Frontmatter（兩種格式共用）

```yaml
---
type: tech-stack-entry
category: {見上方有效分類值}
updated: {YYYY-MM-DD}
---
```
「第三方服務」分類額外選填 `project`（首次記錄來源專案，無則填 `—`）。

### 精簡格式（後端框架／資料庫／雲端/基礎設施／前端／DevOps）

```markdown
# {技術名稱}

**使用過的版本**：
**踩過的坑**：
**使用過的專案**：
```
`適用情境`、`推薦配置`、`常用服務`、`費用注意`、`常用 pattern` 為選填欄位，依技術性質挑選相關的加入。

### 完整格式（第三方服務）

```markdown
# {服務名稱}（{用途}）

**官方文件**：{URL}
**使用過的版本/方案**：
**使用過的專案**：

#### ⚠️ 踩過的坑

#### ✅ 有效配置

#### 📌 整合注意事項

#### 🔗 相關 Pattern / 教訓
```

---

## 必填欄位

| 欄位 | 必填 | 說明 |
|------|------|------|
| frontmatter `category` | ✅ | 須在「有效分類值」列表中 |
| frontmatter `updated` | ✅ | YYYY-MM-DD 格式 |
| `**踩過的坑**` 或對應的「⚠️ 踩過的坑」區塊 | ⬜ 選填 | 空白視為完整度 ⬜（尚未累積實戰記錄，非缺陷） |
| `**使用過的專案**` | ⬜ 選填 | 同上 |

技術筆記是從實戰累積的記錄，新建立時本就允許空白；「未填寫」不算格式錯誤，只在 `/health-check` 完整度統計中呈現。

---

## 健康檢查規則（供 /health-check 使用）

一份 `tech-stack/{slug}.md` 被視為「不健康」（格式錯誤，非空白）如果：
- 缺少 frontmatter 或 frontmatter 缺少 `category`、`updated`
- `category` 不在「有效分類值」列表中
- `updated` 格式不是 YYYY-MM-DD
- `index.md` 中找不到對應該檔案的行（登記遺漏）

完整度統計（非錯誤，僅供 `/self-improve` 參考）：
- 內容欄位（踩過的坑／有效配置等）全部空白 → `index.md` 完整度標記 ⬜
- 部分填寫 → 🟡；核心欄位皆有內容 → ✅
