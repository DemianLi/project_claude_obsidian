# Phase 3：更新 CHANGELOG（最終版本記錄）

在 `projects/{專案}/CHANGELOG.md` append：

```markdown
## [{最終版本}] — {YYYY-MM-DD}（專案收尾）

### 交付項目
{從 functional.md 列出所有已完成需求}
- ✅ {REQ-ID}：{需求名稱}

### 已知問題（遺留至結案）
{Phase 1 中記錄的遺留問題，若選項 B}
{若無：「無遺留問題，所有項目已完成或關閉。」}

### 收尾備注
{使用者提供的說明，或 Claude 自動摘要}
```

若 CHANGELOG.md 不存在，先建立再 append。

→ 完成後讀取 `_close-project/wiki.md`
