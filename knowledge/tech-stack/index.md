---
type: tech-stack-index
updated: 2026-06-27
---

# 技術棧筆記 ⚡ 薄索引

> 累積各技術的使用心得、陷阱和最佳配置。從實際專案中學到的，不是教科書內容。
> Claude 先讀此表比對關鍵字，只讀有交集的個別檔案，跳過無關的。
>
> **Claude 在以下時機查閱：**
> - BEFORE CODING：任務涉及外部 API / 第三方服務整合時，依關鍵字查對應條目
> - `/research`：搜索技術方案前，先比對避免重複踩坑
> - `/self-improve`：從 dev-notes 提取新踩坑後，更新對應條目或新增一行

| 項目 | 類型 | 檔案 | 關鍵字 | 使用次數 | 最後使用 | 完整度 |
|------|------|------|--------|---------|---------|--------|
| LINE Pay | 🔌 第三方服務 | [line-pay.md](line-pay.md) | line pay, 支付, 金流 | 0 | — | ⬜ 空白 |
| Node.js / Express | 🖥 後端框架 | [nodejs-express.md](nodejs-express.md) | node, express | 0 | — | ⬜ 空白 |
| PHP / Laravel | 🖥 後端框架 | [php-laravel.md](php-laravel.md) | php, laravel | 0 | — | ⬜ 空白 |
| MySQL | 🗄 資料庫 | [mysql.md](mysql.md) | mysql | 0 | — | ⬜ 空白 |
| PostgreSQL | 🗄 資料庫 | [postgresql.md](postgresql.md) | postgres, postgresql | 0 | — | ⬜ 空白 |
| AWS | ☁️ 雲端/基礎設施 | [aws.md](aws.md) | aws, ec2, s3 | 0 | — | ⬜ 空白 |
| React / Next.js | 🎨 前端 | [react-nextjs.md](react-nextjs.md) | react, next.js | 0 | — | ⬜ 空白 |
| Docker | 🔧 DevOps | [docker.md](docker.md) | docker | 0 | — | ⬜ 空白 |

<!-- 新增技術時：在此表追加一行 + 建立對應 {slug}.md（依新增的記錄格式），/self-improve 時更新使用次數/最後使用 -->

---

## 🏢 甲方特殊環境

> 記錄特定甲方的環境限制，避免設計出跑不起來的方案。規模小，留在索引內不另拆檔。

| 甲方 | 環境限制 | 已驗證的解法 | 來源專案 |
|------|----------|------------|---------|
| — | — | — | — |

---

## 個別檔案格式（建立 `{slug}.md` 時使用）

**第三方服務 / 外部 API**（最重要，踩坑最容易跨專案重複）：
```markdown
**官方文件**：{URL}
**使用過的版本/方案**：{v3 / Sandbox / 正式環境}
**使用過的專案**：{專案名}（{YYYY-QN}）

#### ⚠️ 踩過的坑
**坑-001：{一句話標題}**
- 現象：{描述發生了什麼}
- 根因：{為什麼會這樣}
- 解法：{怎麼解決}
- 發現於：{專案名}，{YYYY-MM-DD}

#### ✅ 有效配置
- {配置項}：{值或說明}

#### 📌 整合注意事項
- {Rate limit / Webhook / 憑證管理 / 環境差異等}

#### 🔗 相關 Pattern / 教訓
- [[knowledge/patterns/index#PAT-XXX]]（若有對應 pattern）
- [[knowledge/lessons-learned/index#LESSON-XXX]]（若有對應教訓）
```

**語言/框架/資料庫/雲端/前端/DevOps**（較通用，格式精簡）：
```markdown
**使用過的版本**：
**適用情境**：
**常見陷阱**：
**推薦配置**：
**使用過的專案**：
```
