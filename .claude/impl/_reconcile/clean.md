# Phase 4：執行清理（人工確認後）+ 完成回報

依使用者的選擇執行以下操作：

## 標記完全解決
更新對應 `_pending/PENDING-{N}.md`（檔案保留，不刪除）：
```markdown
**狀態**：✅ 已解決（{YYYY-MM-DD}）
**解決方式**：由 REQ-FXXX、REQ-FXXX 涵蓋
```
並從 `_pending/_index.md` 目錄移除該行。

## 拆分部分解決的條目
更新原檔案 `_pending/PENDING-{N}.md`：
```markdown
**狀態**：🔶 部分解決（{YYYY-MM-DD}）
**已解決**：{已解決部分}，見 REQ-FXXX
**剩餘問題**：→ 見 PENDING-{新N}（繼承自本條）
```
新建 `_pending/PENDING-{新N}.md`（繼承自 PENDING-{N}），並登記至 `_pending/_index.md` 目錄。

## 合併內部重複
保留較完整的條目檔案，另一份標記「已合併至 PENDING-{N}」，並從 `_pending/_index.md` 目錄移除。

---

## 完成回報

```
✅ 對帳完成｜專案：{名稱}

清理結果：
  標記完全解決：{N} 條
  拆分部分解決：{N} 條 → 新增 {N} 條繼承項目
  合併重複：{N} 組
  仍待釐清：{N} 條

知識庫健康度：
  _pending/：{N} 條（已解決 {N} / 未解決 {N}）
  _inferred/：{N} 條推測 + {N} 個缺口

📌 剩餘待辦：
  - 超過 30 天未釐清：{N} 條（建議主動追問甲方）
  - 邏輯缺口仍開放：{N} 個（擴充相關功能前必須解決）
```

append 記錄至 `wiki/log.md`。
