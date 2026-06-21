---
type: system-design
project: _example
updated: 2026-06-21
---

# 系統設計

---

## 架構總覽

{描述整體架構，例如：三層架構、微服務、Event-driven 等}

```
[前端 SPA]
    ↓ HTTPS
[API Gateway / Load Balancer]
    ↓
[後端服務]
    ├── [Service A]
    └── [Service B]
         ↓
[資料庫]    [外部 API]
```

---

## 主要組件

### {組件一}
- **職責**：
- **技術選擇**：
- **相關 ADR**：[[../04-decisions/ADR-XXX]]

### {組件二}
- **職責**：
- **技術選擇**：

---

## 資料流

### {流程一：例如用戶登入}
1. 前端送出 `POST /api/auth/login`
2. 後端驗證憑證
3. 回傳 JWT token

---

## 資料模型

### {Entity 一}
```
{EntityName}
├── id: UUID
├── created_at: timestamp
└── ...
```

---

## 安全設計

{描述身份驗證、授權流程、資料保護機制}

---

## 擴展性考量

{描述如何應對用戶增長、資料量增長}

---

## 已知技術債

| 項目 | 原因 | 預計處理時間 |
|------|------|-------------|
| — | — | — |
