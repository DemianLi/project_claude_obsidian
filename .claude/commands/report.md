---
description: 產生專案進度報告（markdown 或甲方可讀格式）
---
# /report — 進度報告生成

## 觸發方式
```
/report                    （生成本週進度報告，對象：甲方）
/report --internal         （生成內部技術進度報告）
/report --period [起～迄]  （指定時間範圍）
/report --format email     （輸出可直接貼入 email 的格式，預設）
/report --format markdown  （輸出 markdown 格式，存入檔案）
```

## 前置條件
```
[ ] wiki/log.md 存在
[ ] projects/{專案}/01-requirements/functional-index.md 存在
[ ] projects/{專案}/00-overview.md 存在
```

## 執行序列（每次只讀當前 Phase 的子文件）

| Phase | 讀取 | 說明 |
|-------|------|------|
| 1 | `_report/read.md` | 讀取資料來源（6 個文件） |
| 2 | `_report/summarize.md` | 彙整：完成度 + blockers + 技術風險 |
| 3 | 無旗標/`--format email` → `_report/generate-external.md`；`--internal` → `_report/generate-internal.md` | 產生報告（兩種格式互不載入） |
| 4 | `_report/output.md` | 輸出：email 格式 / 存檔 / log 記錄 |

## 路由規則
- 無旗標 / `--format email` → 對外格式
- `--internal` → 內部技術格式
- 未指定專案 → Phase 1 詢問「這份報告要涵蓋哪個專案？」
