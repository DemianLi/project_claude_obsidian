---
type: patterns-index
updated: 2026-06-21
---

# 設計模式庫

> 從實際專案中提煉出的可複用解法。每個模式都有「在哪個專案驗證過」的記錄。

---

## ⚡ 精準讀取表（Claude 先讀此表，只讀相關條目）

<!-- Claude 讀取規則：
  1. 讀此表 → 比對當前任務關鍵字與 Tags 欄位
  2. 只讀取 Tags 有交集的 PAT 條目，跳過無關的
  3. 只推薦 status=validated 或 experimental；status=deprecated → 告知已棄用
-->

| PAT-ID | 標題 | Tags（比對關鍵字） | Status | 有驗證 |
|--------|------|-----------------|--------|--------|
| PAT-AUTH-001 | JWT + Refresh Token | authentication, jwt, security, rest-api | experimental | ❌ |
| PAT-DB-001 | Repository Pattern | database, orm, testability, clean-arch | experimental | ❌ |
| PAT-API-001 | 統一錯誤回應格式 | api, error-handling, rest-api, client-facing | experimental | ❌ |

<!-- /save 時自動 append 新 pattern 至此表格（同時在下方加完整條目） -->

---

## 如何使用

在開始實作新功能前，先讀上方精準讀取表比對 Tags，找到相關 PAT 後再讀完整條目。  
Claude 在 `/self-improve` 時會自動從 dev-notes 提取新模式加入此文件。

**格式 schema**：`knowledge/_schemas/pat.md`

---

## 認證與授權

### PAT-AUTH-001：JWT + Refresh Token 標準實作

---
tags: [authentication, jwt, security, stateless, rest-api, cookie]
status: experimental
projects: []
---

**驗證次數**：0 次（預設模式，尚待第一個專案驗證）
**適用情境**：需要無狀態身份驗證的 REST API，且前後端分離  
**不適用情境**：Server-side rendering 為主的傳統 MPA（Session 更簡單）
**參考工時**：初次實作約 8-12 小時；複用模式約 4-6 小時

#### 實作要點

```
Access Token：15 分鐘有效期
Refresh Token：7 天，單次使用，輪換機制（rotation）
Storage：HttpOnly Cookie（防 XSS）
Server 端儲存：Refresh Token 需存 DB 以支援撤銷
```

#### 注意事項

- Refresh Token 需要 DB 儲存以支援登出和撤銷
- 多設備登入需要多個 Refresh Token per user
- 跨域（CORS）時 Cookie 需設定 `SameSite=None; Secure`

#### 相關資源

- **相關教訓**：（待填入——串接後若踩坑補充）
- **相關 ADR**：（若有選擇此方案的 ADR 記錄，填入）

---

## 資料存取

### PAT-DB-001：Repository Pattern

---
tags: [database, abstraction, testability, architecture, orm]
status: experimental
projects: []
---

**驗證次數**：0 次（預設模式）
**適用情境**：需要抽象 DB 操作、方便測試的後端服務；預期未來可能換 ORM 或 DB
**不適用情境**：小型快速開發（CRUD 簡單的 prototype），overhead 大於收益
**參考工時**：初次搭建 Repository 層約 4-8 小時；後續每個 entity 約 1-2 小時

#### 實作要點

```
Service → Repository Interface → Repository Implementation → DB
```

#### 注意事項

- 小專案 overhead 高，在決定使用前評估是否有測試需求
- Repository Interface 要夠薄，不要把 SQL 語法泄漏到 interface 層

#### 相關資源

- **相關教訓**：（待填入）

---

## API 設計

### PAT-API-001：統一錯誤回應格式

---
tags: [api, rest-api, error-handling, response-format, consistency]
status: experimental
projects: []
---

**驗證次數**：0 次（預設模式）
**適用情境**：所有 REST API 專案，前後端分離
**不適用情境**：純 server-side 渲染，錯誤直接渲染 HTML 頁面
**參考工時**：定義格式約 1 小時；整合至全專案約 2-4 小時

#### 實作要點

```json
{
  "error": {
    "code": "SNAKE_CASE_CODE",
    "message": "使用者可讀訊息（中文或英文視甲方需求）",
    "details": {}
  }
}
```

#### 注意事項

- `code` 欄位要全大寫 SNAKE_CASE，方便前端 switch-case
- `message` 要有意義，不能直接暴露 DB 錯誤訊息

#### 相關資源

- **相關教訓**：（待填入）

---

## 待提取模式

> 未來從 dev-notes 提取後放在這裡

| 主題 | 來源專案 | 日期 | 建議 Tags |
|------|----------|------|-----------|
| — | — | — | — |
