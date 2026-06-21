---
type: api-contracts
project: _example
updated: 2026-06-21
---

# API 規格

---

## 通用規範

- Base URL：`{https://api.example.com/v1}`
- 認證：`Authorization: Bearer {token}`
- 回應格式：JSON
- 錯誤格式：
  ```json
  {
    "error": {
      "code": "ERROR_CODE",
      "message": "Human readable message"
    }
  }
  ```

---

## 端點清單

### POST /auth/login

**說明**：用戶登入  
**需求引用**：[[../01-requirements/functional#REQ-F001]]

**Request:**
```json
{
  "email": "string",
  "password": "string"
}
```

**Response 200:**
```json
{
  "token": "string",
  "expires_at": "ISO8601"
}
```

**Error Codes:**
| Code | HTTP | 說明 |
|------|------|------|
| INVALID_CREDENTIALS | 401 | 帳密錯誤 |
| ACCOUNT_LOCKED | 403 | 帳戶鎖定 |

---

### GET /users/{id}

**說明**：取得用戶資料  
**需求引用**：

**Request Headers:**
- `Authorization: Bearer {token}`

**Response 200:**
```json
{
  "id": "uuid",
  "name": "string",
  "email": "string"
}
```

---

## 版本紀錄

| 版本 | 日期 | 變更 |
|------|------|------|
| v1.0 | — | 初版 |
