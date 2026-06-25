---
tags: [api, rest-api, error-handling, response-format, consistency]
status: experimental
projects: []
---

# PAT-API-001：統一錯誤回應格式

**驗證次數**：0 次（預設模式）
**適用情境**：所有 REST API 專案，前後端分離
**不適用情境**：純 server-side 渲染，錯誤直接渲染 HTML 頁面
**參考工時**：定義格式約 1 小時；整合至全專案約 2-4 小時

## 實作要點

```json
{
  "error": {
    "code": "SNAKE_CASE_CODE",
    "message": "使用者可讀訊息（中文或英文視甲方需求）",
    "details": {}
  }
}
```

## 注意事項

- `code` 欄位要全大寫 SNAKE_CASE，方便前端 switch-case
- `message` 要有意義，不能直接暴露 DB 錯誤訊息

## 相關資源

- **相關教訓**：（待填入）
