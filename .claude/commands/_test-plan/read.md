# Phase 1：讀取需求

讀取 `projects/{專案}/01-requirements/functional.md`，篩選：
- 狀態為 `✅ 已確認甲方` 的需求
- 若指定 REQ-ID 或 `--scope {功能名}`，只取對應的需求

同時讀取：
```
03-client-context/domain-knowledge.md → 確認領域術語，避免測試案例誤用甲方特定術語
06-qa-testing/ 目錄 → 是否已有現有測試計畫
```

若已有現有測試計畫（`test-plan-*.md`）：
- 讀取現有計畫，**避免重複生成已存在的測試案例**
- `--update` 模式：只生成新需求的測試案例，不覆蓋現有案例

篩選結果統計：
```
✅ 已確認需求（可生成測試）：{N} 條
🕐 待確認需求（跳過）：{N} 條
❌ 已廢棄需求（跳過）：{N} 條
現有測試案例（已存在，不重複生成）：{N} 個
```

→ 完成後讀取 `_test-plan/generate.md`
