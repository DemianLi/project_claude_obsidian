---
description: 記錄 bug 或批次處理 UAT 回饋（--uat / --list / --close）
---
# /bug — 快速記錄 Bug

## 觸發方式
```
/bug [問題描述]             （快速記錄單一 bug）
/bug TC-{ID} [問題描述]    （從失敗測試案例記錄 bug）
/bug --uat [甲方回饋文字]  （UAT 批次回饋分流）
/bug --list                 （列出所有未關閉的 bug）
/bug --close BUG-{N}       （標記 bug 已修復並關閉）
```

## 前置條件
```
[ ] projects/{專案}/06-qa-testing/bugs.md 存在
     （若不存在：詢問「bugs.md 不存在，要現在建立嗎？」）
[ ] projects/{專案}/01-requirements/functional.md 存在
--uat 額外：functional.md 至少有 1 條 ✅ 已確認甲方 的需求
--list / --close：bugs.md 存在（若不存在：回報「此專案尚無 bug 記錄」）
```

## 執行路由（先看 $ARGUMENTS，直接路由，不詢問）

| $ARGUMENTS 包含 | 讀取 | 說明 |
|----------------|------|------|
| `--uat` | `{KB_ROOT}/.claude/impl/_bug/uat.md` | UAT 批次回饋分流（U-1 ～ U-6） |
| 其他（描述文字 / `TC-{ID}` / `--list` / `--close`） | `{KB_ROOT}/.claude/impl/_bug/quick.md` | 快速記錄 + 列表 + 關閉 |

## 與其他指令的關係
```
問題來源
  ├─ 單一問題 / TC 失敗 → /bug [描述] → bugs.md
  ├─ UAT 甲方批次回饋 → /bug --uat
  │   ├─ 🔧 實作缺陷 → bugs.md
  │   ├─ 📋 需求誤解 → _pending.md
  │   └─ 🆕 新需求 → /cr
  └─ 修復後 → /bug --close BUG-N
```
