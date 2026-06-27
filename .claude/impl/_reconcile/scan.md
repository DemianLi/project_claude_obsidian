# Phase 2：語意比對掃描

對 `_pending/` 和 `_inferred/` 下每個條目檔案，與相關 `functional/{module}.md` 做語意比對：

| 比對結果 | 說明 |
|----------|------|
| 🟢 已被涵蓋 | functional/{module}.md 中有對應的確認需求，語意相符 |
| 🟡 部分重疊 | functional/{module}.md 涵蓋了部分，仍有未解決的疑問 |
| ⚪ 無對應 | functional/{module}.md 中找不到語意相關的確認需求 |

同時進行**內部去重**：掃描 `_pending/` 和 `_inferred/` 內部各檔案是否有重複描述同一問題的條目。

掃描完成後，建立以下清單：
- 🟢 已被涵蓋的條目清單（可建議解決）
- 🟡 部分重疊的條目清單（需拆分或確認）
- ⚪ 無對應的條目清單（仍需甲方釐清）
- ♻️ 內部重複的條目組（可建議合併）

→ 完成後讀取 `_reconcile/report.md`
