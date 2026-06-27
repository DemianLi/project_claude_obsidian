# /export --client — 甲方交付文件

## Phase 1：讀取來源
```
1. {專案}/00-overview.md          → 專案名稱、目標、甲方資訊
2. {專案}/01-requirements/functional-index.md → 各 functional/{module}.md，取得需求與完成狀態
3. {專案}/02-architecture/api-contracts/index.md → 各群組 API 清單
4. {專案}/06-qa-testing/test-plan-*.md → 測試結果（若有）
5. {專案}/CHANGELOG.md            → 版本紀錄
```

## Phase 2：詢問輸出細節
```
① 交付的系統版本號？（例：v1.0.0）
② 是否包含 API 文件？（Y/n）
③ 是否包含測試報告摘要？（Y/n）
④ 甲方聯絡人姓名（收件人）？
```

## Phase 3：生成文件

儲存至：`projects/{專案}/06-qa-testing/delivery-doc-v{版本}.md`

文件結構：
```
一、系統概述（從 overview 提取，甲方語言）
二、功能清單（需求 → 驗收狀態表格）
    | 功能名稱 | 說明 | 合約版本 | 驗收狀態 |
三、系統環境需求（從 existing-system 提取）
四、API 清單（若包含，摘要格式）
    | 功能 | 方法 | 端點 | 說明 |
五、測試報告摘要（若包含，通過率 + 已知問題）
六、版本紀錄（從 CHANGELOG 提取）
七、後續維護說明（備份、日誌清理、常見問題排查）
附件清單
```

## 完成回報
```
✅ 交付文件已生成
📄 06-qa-testing/delivery-doc-v{版本}.md
包含：功能清單（{N} 條）｜API（{N} 個端點）｜測試摘要
⚠️ 已知問題：{N} 個（建議交付前修復 🔴 高優先的 {N} 個）
```
