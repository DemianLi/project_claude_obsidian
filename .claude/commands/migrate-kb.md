---
description: 遷移舊格式知識庫至現行結構
---
# /migrate-kb — 遷移專案至模組索引格式

## 觸發方式
```
/migrate-kb {專案名稱}                    （遷移所有可遷移的部分）
/migrate-kb {專案名稱} --dry-run          （只分析不寫入，確認計畫）
/migrate-kb {專案名稱} --target=reqs      （只遷移需求模組化）
/migrate-kb {專案名稱} --target=arch      （只遷移架構元件化）
/migrate-kb {專案名稱} --target=api       （只遷移 API 群組化）
```

## 適用時機
當 BEFORE CODING 提示「建議執行 /migrate-kb」時，或知識庫使用舊格式（扁平單檔案）時。

## 前置條件
```
[ ] projects/{專案}/ 存在
--target=reqs：functional.md 存在，functional-index.md 尚未存在
--target=arch：system-design.md 存在，system-design/ 目錄尚未存在
--target=api：api-contracts.md 存在，api-contracts/ 目錄尚未存在
```

## 執行序列（每次只讀當前 Phase 的子文件）

| Phase | 讀取 | 說明 |
|-------|------|------|
| 1 | `_migrate-kb/analyze.md` | 分析現有文件，建議模組分組（等待確認） |
| 2 | `_migrate-kb/reqs.md` | --target=reqs：建立 functional/ 模組結構 |
| 3 | `_migrate-kb/arch-api.md` | --target=arch / --target=api：元件化 / 群組化 |
| 4 | `_migrate-kb/done.md` | 驗證 + 更新索引 + 完成回報 |

> `--dry-run` 模式：只執行 Phase 1 後停止，不寫入任何檔案。
