---
description: 對帳知識庫需求紀錄與現實落差
---
# /reconcile — 知識庫全面對帳與清理

## 觸發方式
```
/reconcile              （掃描當前活躍專案）
/reconcile [專案名稱]   （指定專案）
```

## 使用時機
- `_pending.md` 或 `_inferred.md` 累積超過 10 條未解決項目
- 連續 `/ingest` 多份文件後
- 逆向工程分析結束、第一批甲方確認資訊進來後

## 核心原則
**語意比對，而非關鍵字比對。** Claude 只提出「這兩條可能有關係」，
由你決定是解決、部分解決還是無關。**Claude 不自動刪除或移動任何條目。**

## 前置條件
```
[ ] projects/{專案}/01-requirements/functional.md 存在
[ ] projects/{專案}/01-requirements/_pending.md 存在
[ ] projects/{專案}/01-requirements/_inferred.md 存在
```

## 執行序列（每次只讀當前 Phase 的子文件）

| Phase | 讀取 | 說明 |
|-------|------|------|
| 1 | `_reconcile/inventory.md` | 清點現況 + 標記高風險項目 |
| 2 | `_reconcile/scan.md` | 語意比對掃描（三種結果） |
| 3 | `_reconcile/report.md` | 呈現對帳報告（等待確認） |
| 4 | `_reconcile/clean.md` | 執行清理（人工確認後）+ 完成回報 |
