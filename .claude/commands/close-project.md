---
description: 專案收尾：快照、CHANGELOG、封存
---
# /close-project — 專案收尾與封存

## 觸發方式
```
/close-project {專案名稱}
/close-project {專案名稱} --archive    （完成後移至 _archive/）
```

## 前置條件
```
[ ] projects/{專案名}/ 目錄存在
[ ] wiki/index.md 中此專案列為「🔄 進行中」
[ ] 00-overview.md 存在
[ ] 01-requirements/functional.md 存在
⚠️ 警示但不阻止：CHANGELOG.md 不存在 / bugs.md 不存在
```

## 執行序列（每次只讀當前 Phase 的子文件）

| Phase | 讀取 | 內容 | 等待確認 |
|-------|------|------|----------|
| 1 | `_close-project/gaps.md` | 收尾確認（未完成需求/bug/pending） | ✅ 必須 |
| 2 | `_close-project/snapshot.md` | 交付文件快照 | ✅ 必須 |
| 3 | `_close-project/changelog.md` | 更新 CHANGELOG 最終版本 | 自動 |
| 4 | `_close-project/wiki.md` | 更新 wiki/index + hot + log | 自動 |
| 5 | `_close-project/archive.md` | 歸檔（`--archive` 時執行）+ 完成回報 | ✅ 確認歸檔 |
