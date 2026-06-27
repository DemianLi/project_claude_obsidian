# Phase 2：層次一 — 結構性事實提取

這些是**程式碼明確告訴我們的**，不需要推測。

## 資料庫分析（若有 schema）

```
Tables 清單與用途推測：
  {表名}          → {用途推測}（主鍵：{pk}，{特殊欄位標記}）

索引與關聯：
  {表名}.{欄位}   → FK to {表名}.{欄位}

特殊欄位標記：
  deleted_at      → 軟刪除
  {ENUM 欄位}     → ENUM('{值1}','{值2}'...)（共 {N} 種狀態）
```

## API 路由分析（若有路由或 controller）

```
已確認存在的端點：
  {METHOD} {路徑}  → {推測功能}

未見對應端點（可能缺失）：
  {METHOD} {路徑}  → 無此路由，但 {有對應資料或邏輯} 暗示可能存在
```

## 知識庫儲存原則（提醒）

| 儲存什麼 | 不儲存什麼 |
|----------|------------|
| Table 名稱、欄位清單、ENUM 值（結構摘要） | 完整 DDL / CREATE TABLE |
| API 路由清單（method + path + 說明） | 完整 controller 程式碼 |
| 狀態機 ASCII 圖 | 完整狀態轉換程式碼 |

→ 以上結果將寫入 `02-architecture/_legacy-analysis.md`（在 Phase 5 確認後）

→ 完成後讀取 `_reverse-engineer/infer.md`
