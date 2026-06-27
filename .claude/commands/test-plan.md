---
description: 從已確認需求自動產生測試計畫
---
# /test-plan — 測試計畫自動生成

## 觸發方式
```
/test-plan                   （為所有未測試的確認需求生成測試計畫）
/test-plan REQ-F{N}          （為單一需求生成測試情境）
/test-plan --scope {功能名}  （為功能模組生成測試計畫）
/test-plan --update          （更新現有測試計畫，加入新需求）
```

## 前置條件
```
[ ] projects/{專案}/01-requirements/functional.md 存在
    且至少有 1 條 ✅ 已確認甲方 的需求
[ ] projects/{專案}/06-qa-testing/ 目錄存在
```

## 執行序列（每次只讀當前 Phase 的子文件）

| Phase | 讀取 | 說明 |
|-------|------|------|
| 1 | `_test-plan/read.md` | 讀取需求 + 領域術語 + 現有測試計畫 |
| 2 | `_test-plan/generate.md` | 為每條需求生成正向/負向/邊界測試情境 |
| 3 | `_test-plan/write.md` | 生成測試計畫文件 + 完成回報 |

## 測試情境格式（預覽）
```
TC-{需求ID}-{序號}：{情境標題}
類型：正向 / 負向 / 邊界 / 效能
對應需求：{REQ-ID}
前置條件 → 步驟 → 預期結果
測試狀態：⬜ 未測 / ✅ 通過 / ❌ 失敗 / ⏭️ 跳過
```
