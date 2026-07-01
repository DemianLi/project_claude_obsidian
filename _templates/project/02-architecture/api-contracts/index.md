---
type: api-contracts-index
project: {project_name}
updated: {YYYY-MM-DD}
---

# API 規格索引

<!-- ⚡ Claude 讀取規則：
  1. 讀此索引 → 比對任務關鍵字 → 識別相關 API 群組
  2. 只讀 api-contracts/{module}.md，不讀其他群組
  3. 若任務不涉及 API 設計或端點確認 → 跳過整個 api-contracts/ 目錄
-->

---

## 📌 API 概況

| 欄位 | 數值 |
|------|------|
| **端點總數** | {N} 個 |
| **已文件化** | {N} 個 |
| **版本** | v{N.N} |
| **Base URL** | `{https://api.example.com/v1}` |
| **認證方式** | {JWT Bearer / API Key / OAuth 2.0} |

---

## 群組目錄

<!--
每個群組一行，格式：
- **{群組名}** → `api-contracts/{檔案名}.md`（{N} 個端點）
  關鍵字：{逗號分隔的任務關鍵字}
  方法：{GET/POST/PUT/DELETE 組合}
新增群組時追加一行
-->

（目前無）

---

## 快速定位規則（Claude 使用）

<!-- 每建立一個群組，依其任務關鍵字在下方補上一條規則 -->

```
（目前無群組，尚無定位規則。建立第一個群組後依上方格式補上。）

若任務是「純後端邏輯/DB 操作」，不涉及 API 端點 → 跳過此目錄
若任務跨多個群組 → 分別讀取各相關群組檔案
```

---

## 通用規格（所有端點適用）

| 欄位 | 規格 |
|------|------|
| **Content-Type** | `application/json` |
| **時區** | {UTC+8（台灣）} |
| **分頁格式** | `?page={N}&per_page={N}` |
| **錯誤回應格式** | 見下方 |

### 統一錯誤回應格式

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "人類可讀的錯誤說明",
    "details": {}
  }
}
```

| HTTP Status | 語意 |
|-------------|------|
| 200 | 成功 |
| 400 | 請求格式錯誤 |
| 401 | 未認證 |
| 403 | 無權限 |
| 404 | 資源不存在 |
| 422 | 業務邏輯驗證失敗 |
| 500 | 伺服器錯誤 |

---

## 檔案清單

```
02-architecture/api-contracts/
├── index.md           ← 你在這裡（永遠先讀）
├── README.md          ← 說明群組結構
└── {slug}.md          ← 各群組端點規格（建立群組時新增）
```
