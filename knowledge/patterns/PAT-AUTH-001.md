---
tags: [authentication, jwt, security, stateless, rest-api, cookie]
status: experimental
projects: []
---

# PAT-AUTH-001：JWT + Refresh Token 標準實作

**驗證次數**：0 次（預設模式，尚待第一個專案驗證）
**適用情境**：需要無狀態身份驗證的 REST API，且前後端分離
**不適用情境**：Server-side rendering 為主的傳統 MPA（Session 更簡單）
**參考工時**：初次實作約 8-12 小時；複用模式約 4-6 小時

## 實作要點

```
Access Token：15 分鐘有效期
Refresh Token：7 天，單次使用，輪換機制（rotation）
Storage：HttpOnly Cookie（防 XSS）
Server 端儲存：Refresh Token 需存 DB 以支援撤銷
```

## 注意事項

- Refresh Token 需要 DB 儲存以支援登出和撤銷
- 多設備登入需要多個 Refresh Token per user
- 跨域（CORS）時 Cookie 需設定 `SameSite=None; Secure`

## 相關資源

- **相關教訓**：（待填入——串接後若踩坑補充）
- **相關 ADR**：（若有選擇此方案的 ADR 記錄，填入）
