---
description: 分析需求或架構變更的影響範疇
---
# /impact — 需求影響範疇分析

## 觸發方式
```
/impact [需求描述]        （分析新需求的影響範疇）
/impact CR-{N}            （分析特定 CR 的影響範疇）
/impact REQ-F{N}          （分析修改現有需求的影響）
```

## ⚠️ 使用時機（評估後再決定是否實作或核准）
- 甲方提出新功能（搭配 `/cr` 使用）
- 現有需求發生變更（可能牽動架構）
- 乍看「很小」的需求（越「小」越容易低估影響）
- 任何涉及 DB schema 變更的需求

## 前置條件
```
[ ] projects/{專案}/02-architecture/arch-index.md 存在
[ ] projects/{專案}/01-requirements/functional-index.md 存在
```

## 執行序列（每次只讀當前 Phase 的子文件）

| Phase | 讀取 | 說明 |
|-------|------|------|
| 1 | `_impact/read.md` | 讀取背景（架構 + 需求 + ADR） |
| 2 | `_impact/analyze.md` | 四維度分析（資料/API/REQ/ADR） |
| 3 | `_impact/estimate.md` | 複雜度 + 工時估算 |
| 4 | `_impact/report.md` | 輸出報告 + 填入 CR 文件（若搭配 /cr） |

## 整合觸發點（Claude 主動提議執行 /impact）
- BEFORE CODING 發現需求是 CR 版本
- 甲方需求涉及「加欄位、改流程、多一個狀態、把 A 改成 B」
- `/ingest` 解析時發現新需求影響超過 2 個現有需求
