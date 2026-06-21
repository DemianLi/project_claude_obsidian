# Phase 5：歸檔（--archive 旗標時執行）+ 完成回報

## 歸檔確認（僅 --archive 時詢問）

```
是否要將整個專案資料夾移至 _archive/ ？

移動後：
  _archive/{專案名稱}/    （原 projects/{專案名稱}/ 的全部內容）

注意：
- 歸檔後專案不顯示在 wiki/index.md「進行中」
- wiki/index.md「已完成」保留一筆摘要紀錄
- 可隨時 /ingest 回 _archive/ 中的文件

確認歸檔？(Y/n)
```

若確認：`mv projects/{專案名稱}/ _archive/{專案名稱}/`

---

## 完成回報

```
🎉 專案已結案｜{專案名稱}

━━━ 完成摘要 ━━━
📦 交付版本：{版本}
📋 需求完成：{N}/{Total} 條（{M} 條 CR 追加）
🐛 Bug 關閉：{N}/{Total} 個

━━━ 生成的文件 ━━━
📄 甲方交付文件：{路徑}（若有）
📄 技術交接文件：{路徑}（若有）
📝 CHANGELOG 最終版本：{版本}

━━━ 知識庫更新 ━━━
✅ wiki/index.md — 移至「已完成」
✅ wiki/hot.md   — 移出活躍專案
✅ wiki/log.md   — 結案紀錄已寫入
{若 --archive：✅ 專案已移至 _archive/{專案名稱}/}

━━━ 本案學到了什麼 ━━━
{若尚未執行 /self-improve，提醒：}
「建議在 dev-notes 完整後執行一次 /self-improve，
  讓本案的模式和教訓沉澱到 knowledge/ 供後續專案使用。」
```
