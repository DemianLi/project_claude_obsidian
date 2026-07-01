# Phase 5：呈現報告 + 確認後寫入

## 分析報告格式

```
🔬 逆向分析報告｜專案：{名稱}

━━━ 🧱 結構性事實（{N} 項）━━━
  Tables：{N} 個
  API 端點：{N} 個
  → 寫入 _legacy-analysis.md？ (Y/n)

━━━ 🔍 推測業務邏輯（{N} 條）━━━
  🟢 高信心：{N} 條
  🟡 中信心：{N} 條
  🔴 低信心：{N} 條
  → 全部建立 _inferred/{ID}.md（推測）並登記至 _inferred/_index.md？ (Y/n)

━━━ ❓ 邏輯缺口（{N} 個）━━━
  ⚡ 狀態機缺口：{N} 個
  🗃️ 資料孤島：{N} 個
  🔀 矛盾邏輯：{N} 個
  → 全部建立 _inferred/{ID}.md（缺口）並登記至 _inferred/_index.md？ (Y/n)

━━━ 建議問甲方的問題清單 ━━━
  [1] {針對 GAP-001 的問題}
  [2] {針對 INF-001 的問題}
  → 要整理成可以直接寄給甲方的問題清單嗎？ (Y/n)
```

## 使用者確認後的寫入規則

- 結構性事實 → `02-architecture/_legacy-analysis.md`（若不存在則依 `_templates/project/02-architecture/_legacy-analysis.md` 建立）
- 推測 + 缺口 → 各自建立 `01-requirements/_inferred/{ID}.md`（INF-/GAP- 各自一檔），並登記至 `_inferred/_index.md`
- **絕不混用**，尤其不得寫入 `functional/{module}.md`

## 推測升格為確認需求的流程

當甲方驗證了某條推測後：
```
/ingest [甲方的回覆內容]
```
由 `/ingest` 走正式確認流程，將推測升格寫入對應 `functional/{module}.md`，
並在 `_inferred/{ID}.md` 將該條標記為 `✅ 已驗證，見 REQ-FXXX`（同步更新 `_inferred/_index.md`）。

## 完成後

append `wiki/log.md`：
```
### [{日期}] {專案} — 逆向工程分析
- 分析範圍：{檔案清單}
- 結構性事實：{N} 項
- 推測：{N} 條（高/中/低：N/N/N）
- 邏輯缺口：{N} 個
- 待甲方回覆問題：{N} 個
```
