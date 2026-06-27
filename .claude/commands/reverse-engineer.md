---
description: 逆向分析現有系統，推測並記錄隱性需求
---
# /reverse-engineer — 逆向分析現有系統

## 觸發方式
```
/reverse-engineer [檔案路徑或貼上程式碼]   （分析特定程式碼或 schema）
/reverse-engineer --db [schema 內容]        （專門分析資料庫結構）
/reverse-engineer --api [路由或 controller] （專門分析 API 行為）
/reverse-engineer --full                    （全面掃描，建議初次接案時用）
```

## ⚠️ 核心原則：三種知識寫入位置不得混用

| 類型 | 定義 | 寫入位置 |
|------|------|----------|
| 🧱 結構性事實 | 程式碼明確存在的東西（table 名、欄位、API 路由） | `02-architecture/_legacy-analysis.md` |
| 🔍 推測業務邏輯 | Claude 從程式碼**推斷**的業務規則，**可能有誤** | `01-requirements/_inferred/{ID}.md`（推測，登記至 `_inferred/_index.md`） |
| ❓ 邏輯缺口 | 程式碼不完整、矛盾、或有死角的地方 | `01-requirements/_inferred/{ID}.md`（缺口，登記至 `_inferred/_index.md`） |

**Claude 禁止將推測直接寫入 `functional/{module}.md`。**

## 前置條件
```
[ ] projects/{專案}/ 已初始化
[ ] 使用者提供程式碼、schema 或指定檔案路徑
```

## 執行序列（每次只讀當前 Phase 的子文件）

| Phase | 讀取 | 說明 |
|-------|------|------|
| 1 | `_reverse-engineer/confirm.md` | 輸入確認 + 分析目標說明 |
| 2 | `_reverse-engineer/extract.md` | 層次一：結構性事實提取 |
| 3 | `_reverse-engineer/infer.md` | 層次二：推測業務邏輯（標記信心度） |
| 4 | `_reverse-engineer/gaps.md` | 層次三：邏輯缺口識別 |
| 5 | `_reverse-engineer/write.md` | 呈現報告 + 確認後寫入 + 更新 log |
