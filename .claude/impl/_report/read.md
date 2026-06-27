# Phase 1：讀取資料來源

依序讀取以下文件，**不得跳過任何一個**：

```
1. wiki/log.md                              → 指定期間內的操作紀錄
2. {專案}/01-requirements/functional.md    → 需求完成狀態
3. {專案}/01-requirements/_pending.md      → 待甲方回覆（即將成為 blockers）
4. {專案}/00-overview.md                   → 專案里程碑與時程（若有）
5. {專案}/05-dev-notes/                    → 指定期間的開發筆記（掃描日期前綴）
6. {專案}/01-requirements/scope.md         → CR 追加狀態
```

若使用者沒有指定時間範圍：
- 預設：本週（今天往前 7 天）
- 詢問：「這份報告要涵蓋哪個時間範圍？（預設：本週 {起}～{迄}）」

若使用者沒有指定專案：
- 詢問：「這份報告要涵蓋哪個專案？」

→ 完成後讀取 `_report/summarize.md`
