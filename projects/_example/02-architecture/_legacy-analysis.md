---
type: legacy-analysis
project: _example
updated: 2026-06-21
---

# 現有系統逆向分析

> 此檔案記錄從程式碼和資料庫**直接觀察到的結構性事實**。
> 這裡的內容是「系統現在是什麼樣子」，不是「應該是什麼樣子」。
> 業務邏輯推測見 `01-requirements/_inferred.md`。
>
> ⚠️ **儲存原則：描述，不是程式碼本身**
> 此文件儲存對程式碼的**結構化摘要**，不儲存原始程式碼、DDL、或 SQL 語句。
> - ✅ 「orders 表有 status 欄位，ENUM 五種值：pending / processing / shipped / completed / cancelled」
> - ✅ 「POST /api/orders 建立訂單，由 OrderController@store 處理」
> - ❌ 貼入完整的 CREATE TABLE 語句
> - ❌ 貼入完整的 controller 程式碼
>
> 若需要保留關鍵程式碼片段作為推測依據，寫在 `_inferred.md` 的【推測依據】欄位，且只引用最小必要的片段（一兩行），不貼整個函數。

---

## 資料庫結構

### Tables 清單

| Table 名稱 | 推測用途 | 主鍵 | 軟刪除 | 備註 |
|-----------|---------|------|--------|------|
| {table_name} | — | id | 有/無 | — |

### 關鍵關聯

```
{table_a}.{foreign_key} → {table_b}.id
{table_c} ← 多對多 → {table_d}（透過 {pivot_table}）
```

### 重要欄位

| Table | 欄位 | 類型 | 特殊值/ENUM | 備註 |
|-------|------|------|-------------|------|
| orders | status | ENUM | pending, processing, shipped, completed, cancelled | 轉換規則見 _inferred.md |

### 觀察到的資料異常

| 現象 | 影響的 Table/欄位 | 記錄數量 | 見 GAP |
|------|-----------------|---------|--------|
| — | — | — | — |

---

## API 端點清單

| Method | Path | Controller | 說明 | 狀態 |
|--------|------|------------|------|------|
| POST | /api/orders | OrderController@store | 建立訂單 | 正常 |
| — | — | — | — | — |

**未見端點（可能缺失）：**
- {預期存在但找不到的端點}

---

## 狀態機圖（現有邏輯）

```
{狀態A} → {狀態B} → {狀態C}
              ↓
           {狀態D}

已確認轉換：A→B（觸發：xxx）、B→D（觸發：xxx）
缺口：B→C 的觸發條件未知（見 GAP-001）
```

---

## 外部整合

| 系統/服務 | 整合方式 | 用途 | 版本/憑證狀態 |
|----------|---------|------|-------------|
| — | — | — | — |

---

## 分析紀錄

| 日期 | 分析範圍 | 執行者 | 備註 |
|------|---------|--------|------|
| 2026-06-21 | 建立模板 | 系統初始化 | — |
