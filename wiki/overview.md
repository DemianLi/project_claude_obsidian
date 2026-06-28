---
type: meta
title: "Knowledge Base Overview"
updated: 2026-06-28
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
- 最近重大更新：2026-06-28 — 協作鎖定機制擴充至架構元件/API 群組（原 02-architecture 無偵測，現補上）、collab/ 路徑去除多餘 `.claude/` 巢狀層、CLAUDE.md 移除對 Claude 無實際用途的 README 指標

## 核心工作流

```
收到資料   → /ingest → 解析→確認→寫入 projects/ 或 wiki/sources/
開始實作   → BEFORE CODING 漏斗（6 步驟，細節見 `.claude/protocols/before-coding.md`）
知識問題   → /query [quick/standard/deep]
累積知識   → /self-improve → patterns + lessons-learned
結束工程   → /save → hot/{縮寫}.md + log.md + 索引更新
```

## 最佳實踐（細節見對應協定文件，避免雙重維護）

- 第三方服務踩坑的雙寫規則 → 見 `.claude/protocols/wiki-layer.md`
- 好答案歸檔至 `wiki/questions/` 的條件 → 見 `/query` 流程（`_query/standard.md` Step 4）
- Session 結束更新 hot/{縮寫}.md 的邏輯 → 見 `CLAUDE.md`「SAVE SESSION」與 `_save/index.md`
