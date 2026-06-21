---
type: lessons-learned
updated: 2026-06-21
---

# 教訓庫

> 踩過的坑、避免重犯的方式。Claude 在 `/self-improve` 時自動提取並更新此文件。

---

## ⚡ 精準讀取表（Claude 先讀此表，只讀相關條目）

<!-- Claude 讀取規則：
  1. 讀此表 → 比對當前任務的 phase 和 root_cause
  2. 只讀取與當前任務情境相符的 LESSON 條目
  3. 在 BEFORE CODING 時，重點看 phase=requirements 和 root_cause=misunderstanding 的教訓
-->

| LESSON-ID | 標題 | Tags | Phase | Root Cause | Severity |
|-----------|------|------|-------|-----------|---------|
| LESSON-001 | 未確認需求就開始實作 | requirements, confirmation, client-communication | requirements | communication | 🔴 高 |

<!-- /save 時自動 append 新 lesson 至此表格（同時在下方加完整條目） -->

---

## 如何使用

先讀上方精準讀取表，找到與當前情境相符的 LESSON 後再讀完整條目。  
**格式 schema**：`knowledge/_schemas/lesson.md`

---

## LESSON-001：未確認需求就開始實作

---
tags: [requirements, confirmation, client-communication, scope-creep]
phase: requirements
root_cause: communication
severity: 🔴 高（直接影響交付）
status: active
---

**來源專案**：通用  
**發生情境**：甲方口頭說明後直接開工，或認為「就是這個意思」而跳過書面確認  
**問題描述**：實作完成後甲方說「我不是這個意思」，需要重做  
**根本原因**：口頭需求存在理解落差，人對語言的理解受背景知識影響，同一句話不同人有不同理解  
**預防方式**：每條需求都要整理成 functional.md 並讓甲方確認；對話中讓甲方明確說「就是這樣」或「對，就是你說的那個」  
**偵測信號**：需求描述過於模糊（「大概是這樣」「你懂的」「類似 XXX 那種」）；甲方說「你們做就好」而不確認細節  
**實際工時損失**：未記錄（估計 4-20 小時，視重做範圍）

#### 是否已納入系統守衛？

- [x] 已納入 BEFORE CODING 的需求狀態守衛（非 ✅ 狀態的需求不得實作）
- [x] 已納入 `/ingest` Phase 3：模糊需求存 _pending.md，不進 functional.md

#### 相關資源

- **相關 Pattern**：（無直接對應 pattern）
- **相關需求守衛**：CLAUDE.md 的「需求狀態守衛（不得跳過）」section

---

## 技術類

> 從真實專案累積後會在此新增

---

## 溝通類

> 從真實專案累積後會在此新增

---

## 估算類

> 從真實專案累積後會在此新增

---

## 統計

| 類別（phase） | 數量 |
|--------------|------|
| 需求類（requirements） | 1 |
| 開發類（development） | 0 |
| 測試類（testing） | 0 |
| 交付類（delivery） | 0 |
| 溝通類（communication） | 0 |

| 根因（root_cause） | 數量 |
|-------------------|------|
| 誤解（misunderstanding） | 0 |
| 溝通（communication） | 1 |
| 技術（technical） | 0 |
| 流程（process） | 0 |
| 估算（estimation） | 0 |
