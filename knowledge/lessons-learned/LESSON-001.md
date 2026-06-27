---
tags: [requirements, confirmation, client-communication, scope-creep]
phase: requirements
root_cause: communication
severity: 🔴 高（直接影響交付）
status: active
---

# LESSON-001：未確認需求就開始實作

**來源專案**：通用
**發生情境**：甲方口頭說明後直接開工，或認為「就是這個意思」而跳過書面確認
**問題描述**：實作完成後甲方說「我不是這個意思」，需要重做
**根本原因**：口頭需求存在理解落差，人對語言的理解受背景知識影響，同一句話不同人有不同理解
**預防方式**：每條需求都要整理成對應 functional/{module}.md 並讓甲方確認；對話中讓甲方明確說「就是這樣」或「對，就是你說的那個」
**偵測信號**：需求描述過於模糊（「大概是這樣」「你懂的」「類似 XXX 那種」）；甲方說「你們做就好」而不確認細節
**實際工時損失**：未記錄（估計 4-20 小時，視重做範圍）

## 是否已納入系統守衛？

- [x] 已納入 BEFORE CODING 的需求狀態守衛（非 ✅ 狀態的需求不得實作）
- [x] 已納入 `/ingest` Phase 3：模糊需求存 _pending/{ID}.md，不進 functional/{module}.md

## 相關資源

- **相關 Pattern**：（無直接對應 pattern）
- **相關需求守衛**：CLAUDE.md 的「需求狀態守衛（不得跳過）」section
