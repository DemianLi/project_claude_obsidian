# Phase 2：彙整進度資料

## 2-1. 需求完成狀態統計（從 functional-index.md → 各 functional/{module}.md）
```
合約範疇內需求：
  已完成（驗收條件全部勾選）：{N} 條
  實作中（有部分驗收條件勾選）：{N} 條
  尚未開始：{N} 條

追加需求（CR）：
  已核准並完成：{N} 條
  已核准實作中：{N} 條
  評估中：{N} 條
```

## 2-2. 識別 blockers（從 _pending/_index.md → 各 _pending/{ID}.md）
找出狀態為「等待回覆」且**超過 7 天未更新**的項目：
```
⚠️ 等待甲方確認（{N} 項）：
  PENDING-{ID}：{問題摘要}（提出日：{date}，已等待 {N} 天）
```

## 2-3. 技術風險識別（從 _inferred/_index.md → 各 _inferred/{ID}.md）
找出與進行中任務相關的 INF/GAP：
```
🔴 高風險：未解決的邏輯缺口影響進行中功能
🟡 中風險：推測待驗證
🟢 低風險：已確認或不影響當前進度
```

彙整完成，記錄以下供 Phase 3 使用：
- 本期完成的功能清單
- 進行中的功能清單
- 下期計畫
- blockers 清單
- CR 清單（若有）

→ 完成後依旗標讀取：無旗標/`--format email` → `_report/generate-external.md`；`--internal` → `_report/generate-internal.md`
