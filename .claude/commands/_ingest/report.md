# Phase 4：完成回報

---

## 一般流程（已知專案）

```
✅ Ingest 完成｜專案：{名稱}

背景知識：stakeholders {N} ｜ existing-system {N} ｜ domain-knowledge {N}
需求整理：functional.md {N} 條（已確認）｜ _pending.md {N} 條 ｜ 衝突裁決 {N}
對帳：待釐清解決 {N} ｜ 推測升格 {N} ｜ 部分解決保留 {N}

📌 待辦：
  - [ ] 回覆甲方確認 _pending.md 中 {N} 個模糊項目
  - [ ] _pending / _inferred 累積 > 10 條 → 考慮執行 /reconcile
```

## 大型文件（0-D 流程額外資訊）

```
✅ 大型文件 Ingest 完成｜{文件名稱}（{N} 頁）

分批：{N} 批 ｜ 去重合併：{N} 條
模組寫入：functional/{module-01}.md {N} ｜ functional/{module-02}.md {N} ｜ ...
索引：✅ functional-index.md 更新 ｜ ✅ 各模組 REQ 快速掃描表已建立
```

## 重新處理無主文件（從 _unassigned 搬移）

```
✅ 無主文件整理完成
來源：_inbox/_unassigned/{檔案名}  目標：{專案名稱}
已寫入 functional.md：{N} 條 ｜ 存入 _pending.md：{N} 條
原暫存檔已移除。
```

---

Append 記錄至 `wiki/log.md`。
