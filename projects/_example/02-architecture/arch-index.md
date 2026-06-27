---
type: arch-index
project: _example
updated: {YYYY-MM-DD}
---

# 架構元件索引

<!-- ⚡ Claude 讀取規則：
  1. 讀此索引 → 比對下方「系統元件地圖」任務關鍵字 → 識別相關元件
  2. 只讀 system-design/{對應元件}.md，不讀其他元件檔案
  3. api-contracts/index.md 只在需要確認 API 規格時才讀（任務包含「API 呼叫/端點」時），再由其路由至相關群組檔案
  4. _legacy-analysis.md 只在逆向工程 / 整合案才讀
-->

---

## 系統元件地圖

<!-- ⚡ Claude：讀此表 → 比對任務關鍵字 → 只讀對應的元件檔案 -->

| 元件 | 說明 | 詳細檔案 | 任務關鍵字 |
|------|------|---------|-----------|
| **認證服務** | JWT 簽發、驗證、Refresh Token | `system-design/auth.md` | 登入, token, session, 權限, 角色 |
| **訂單系統** | 訂單狀態機、出貨流程 | `system-design/order.md` | 訂單, 出貨, 退款, 取消, 狀態機 |
| **通知模組** | Email/SMS 發送邏輯 | `system-design/notification.md` | 通知, Email, SMS, 推播 |
| **資料庫層** | Schema、ORM、Migration | `system-design/database.md` | 資料庫, table, schema, migration |
| **外部整合** | 第三方服務串接 | `system-design/integration.md` | 串接, webhook, 金流, OAuth, 第三方 |
| **API 規格** | RESTful 端點規格 | `api-contracts/index.md` → 再路由 | API, 端點, request, response, HTTP |

<!-- 新增元件時在此表格追加，同時建立對應的 system-design/{slug}.md 檔案 -->

---

## 架構文件清單

```
02-architecture/
├── arch-index.md                 ← 你在這裡（永遠先讀）
├── system-design/
│   ├── README.md                 ← 說明元件分檔結構
│   ├── auth.md                   ← 認證元件架構
│   ├── order.md                  ← 訂單元件架構
│   └── ...（其他元件）
├── api-contracts/
│   ├── index.md                  ← API 薄索引（先讀）
│   ├── auth.md                   ← 認證 API 端點
│   ├── order.md                  ← 訂單 API 端點
│   └── ...（其他群組）
└── _legacy-analysis.md           ← 逆向工程結果（整合案才讀）
```

---

## 讀取決策樹（Claude 使用）

```
任務描述 → 判斷
  ├─ 包含「登入/Token/權限/角色」
  │   → 讀 system-design/auth.md
  │
  ├─ 包含「訂單/出貨/退款/取消」
  │   → 讀 system-design/order.md
  │
  ├─ 包含「API/端點/HTTP/request/response」
  │   → 讀 api-contracts/index.md
  │   → 由 index.md 路由至相關群組檔案
  │
  ├─ 包含「資料庫/table/schema/migration」
  │   → 讀 system-design/database.md
  │
  ├─ 包含「整合/串接/webhook/第三方」
  │   → 讀 system-design/integration.md
  │   → 若是既有系統整合：同時讀 _legacy-analysis.md
  │
  └─ 跨多個元件 → 分別讀取各相關元件檔案

若 system-design/ 目錄不存在（舊格式）：
  → fallback 讀 system-design.md 全文
  → 提示：「建議執行 /migrate-kb 拆分為元件格式」
```
