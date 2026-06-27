# Phase 4：驗證 + 更新索引 + 完成回報

## 自動核對

- **需求**：原始 functional.md 條數 = 各模組合計條數
- **API**：原始 api-contracts.md 端點數 = 各群組合計端點數

若有差異 → **停止**，列出遺漏項目請使用者確認分配。

## 更新索引（自動執行）

```
functional-index.md   → 更新模組目錄（若執行 --target=reqs）
arch-index.md         → 更新元件地圖（若執行 --target=arch）
api-contracts/index   → 確認群組索引完整（若執行 --target=api）
wiki/hot/{自己的縮寫}.md → 記錄本次遷移
wiki/log.md           → append 遷移記錄
```

## 完成回報

```
✅ 遷移完成｜{專案名稱}

━━━ 需求模組化（--target=reqs）━━━
  📋 需求總數：{N} 條（核對一致）
  📁 建立模組：{N} 個（{模組列表}）
  ⚡ 三層索引：functional-index → Quick Context → REQ 掃描表

━━━ 架構元件化（--target=arch）━━━
  🏗️ 系統元件：{N} 個
  📄 system-design/ 目錄已建立

━━━ API 群組化（--target=api）━━━
  🔌 API 端點：{N} 個（核對一致）
  📁 建立群組：{N} 個

BEFORE CODING 效益（預估）：
  遷移前：讀取全量文件（約 {N} KB）
  遷移後：讀取薄索引 + 相關子集（平均 {N} KB）
  Token 節省：約 60-80%

原始扁平檔案保留為備份（已加遷移說明）。
```
