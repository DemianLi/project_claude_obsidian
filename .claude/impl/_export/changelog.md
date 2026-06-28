# /export --changelog — 版本紀錄

從 `wiki/log.md` 和各 `functional/{module}.md` 提取，
以使用者可選擇的版本範圍生成標準 CHANGELOG 格式。

詢問：
```
① 版本範圍？（例：從 v1.0.0 到 v1.2.0，或「全部」）
② 目標讀者？（甲方 / 內部）
```

更新至：`projects/{專案}/CHANGELOG.md`（append 新版本，不覆蓋舊記錄）

格式：
```markdown
## [v{版本}] — {YYYY-MM-DD}

### 新增功能
- {功能名稱}：{一句話描述}（REQ-FXXX）

### 修改功能
- {功能名稱}：{變更說明}（CR-XXX）

### 修復問題
- {問題描述}（BUG-XXX）

### 已知問題
- {若有}
```
