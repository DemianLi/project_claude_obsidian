# api-contracts/ — API 規格群組目錄

此目錄存放各業務模組的 API 端點規格，是 `index.md` 的深層內容層。

## 讀取規則

Claude **不直接讀取此目錄**，必須先讀 `index.md` 識別相關群組後才讀對應檔案。

## 群組檔案命名

每個業務模組一個 `.md` 檔案，與 `functional/` 的模組命名保持一致：

```
api-contracts/
├── index.md         ← 薄索引（永遠先讀）
├── auth.md          # 認證相關 API（登入、登出、refresh token）
├── order.md         # 訂單相關 API（下單、查詢、取消、出貨）
├── payment.md       # 金流相關 API（付款、退款、對帳）
├── report.md        # 報表相關 API（匯出、統計查詢）
└── ...
```

## 群組檔案結構（每個群組檔案的格式）

```markdown
---
type: api-contracts-module
module: {模組名}
project: {專案名}
updated: {YYYY-MM-DD}
---

# {模組中文名} API 規格

## 📌 Quick Context
<!-- ⚡ Claude：先確認此群組與當前任務相關後才讀 -->
**端點數**：{N} 個（GET: {N}, POST: {N}, PUT: {N}, DELETE: {N}）
**最後更新**：{YYYY-MM-DD}（{新增/修改哪個端點}）
**注意事項**：{若有特殊認證要求或破壞性變更的警告}
<!-- /Quick Context -->

---

## 端點快速查詢表

<!-- ⚡ Claude：先看此表，確認相關端點後只讀對應的端點詳細規格 -->

| 端點 | 方法 | 說明 | 認證 |
|------|------|------|------|
| `/auth/login` | POST | 用 email+密碼登入，取得 token | ❌ 不需要 |
| `/auth/refresh` | POST | 刷新 access token | ✅ Refresh Token |
| `/auth/logout` | DELETE | 登出並使 token 失效 | ✅ Bearer |

---

## 端點詳細規格

### POST /auth/login

**說明**：{端點功能描述}

**Request Body**
\`\`\`json
{
  "email": "user@example.com",
  "password": "string"
}
\`\`\`

**Response 200**
\`\`\`json
{
  "access_token": "eyJ...",
  "refresh_token": "eyJ...",
  "expires_in": 3600
}
\`\`\`

**錯誤**：401 密碼錯誤、422 email 格式不符

**關聯需求**：REQ-F001
```

## 為何拆分群組

- 單一 api-contracts.md 累積至 150+ 端點時，讀取整份文件浪費大量 token
- 群組化後，一個業務模組平均 10–30 個端點，讀取量降至全量的 10–20%
- 端點快速查詢表（在每個群組檔案頂部）讓 Claude 進一步只讀相關端點的詳細規格
