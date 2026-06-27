---
type: meta
title: "Knowledge Base Overview"
updated: 2026-06-22
---

# 知識庫總覽

> 此頁是整個 vault 的執行摘要。每次重大變化後更新。

## 系統架構

此 vault 融合兩層知識體系：

```
【工程層】專案導向，結構嚴謹
projects/   → 各甲方專案：需求/架構/決策/測試
knowledge/  → 跨專案沉澱：patterns / lessons / tech-stack

【Wiki 知識層】個人二腦，複利增長
wiki/concepts/   → 技術概念與框架理解
wiki/entities/   → 工具、服務、平台踩坑記錄
wiki/sources/    → 閱讀筆記、研究資料摘要
wiki/questions/  → 有價值的問答歸檔
.raw/            → 原始文件（不可修改）
```

## 目前狀態（手動更新）

- 進行中專案：見 `wiki/index.md`
- Wiki 頁面數：0（知識層剛建立）
- 最近重大更新：2026-06-27 — 分檔索引架構定為唯一正規（刪除舊扁平檔）、全指令系統路徑修正、CLAUDE.md 壓縮、wiki/hot 與 tech-stack 改為 per-engineer/per-item 分檔

## 核心工作流

```
收到資料   → /ingest → 解析→確認→寫入 projects/ 或 wiki/sources/
開始實作   → BEFORE CODING 精準漏斗（8 stages）
知識問題   → /query [quick/standard/deep]
累積知識   → /self-improve → patterns + lessons-learned
結束工程   → /save → hot/{縮寫}.md + log.md + 索引更新
```

## 最佳實踐

- 任何第三方服務的踩坑 → 同時記錄 `knowledge/tech-stack/` 和 `wiki/entities/`
- 好的查詢答案 → 歸檔至 `wiki/questions/`（≥3 來源的整合答案）
- Session 結束 → `/save` 更新 hot/{縮寫}.md 確保下次 session 有脈絡
