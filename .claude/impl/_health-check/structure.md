# Phase 1：結構完整性檢查

對每個進行中專案（或指定專案），驗證必要檔案是否存在：

```
必要檔案（10 個，各佔 10 分）：
  [ ] 00-overview.md
  [ ] 01-requirements/functional-index.md
  [ ] 01-requirements/scope.md
  [ ] 01-requirements/_pending/_index.md
  [ ] 01-requirements/_inferred/_index.md
  [ ] 02-architecture/arch-index.md
  [ ] 03-client-context/existing-system.md
  [ ] 03-client-context/domain-knowledge.md
  [ ] 03-client-context/stakeholders.md
  [ ] 06-qa-testing/bugs-active.md

加分項（完整度更高但非必要）：
  [ ] 02-architecture/api-contracts/index.md
  [ ] 02-architecture/_legacy-analysis.md
  [ ] 04-decisions/ 至少 1 份 ADR
  [ ] 05-dev-notes/ 至少 1 份 dev session
  [ ] CHANGELOG.md
```

計算每個專案的**結構完整度分數**（必要檔案 / 10 × 100%）。

輸出格式：
```
{專案名}：{N}/10 ✅（{%}）
  缺少：{缺少的檔案列表}

{專案名}：{N}/10 ⚠️（{%}）
  缺少：{缺少的檔案列表}
```

---

## 舊格式殘留偵測（與上方正向 checklist 互補）

上方檢查的是「新格式該有的檔案是否存在」，這裡反向檢查「舊格式扁平檔案是否還殘留、尚未遷移」——這正是 `/migrate-kb` 判斷可否執行的同一組條件，提前在 health-check 主動暴露：

```
[ ] functional.md 存在 且 functional-index.md 不存在
      → ⚠️ 偵測到舊格式殘留，建議 /migrate-kb {專案} --target=reqs
[ ] system-design.md 存在 且 system-design/ 目錄不存在
      → ⚠️ 偵測到舊格式殘留，建議 /migrate-kb {專案} --target=arch
[ ] api-contracts.md 存在 且 api-contracts/ 目錄不存在
      → ⚠️ 偵測到舊格式殘留，建議 /migrate-kb {專案} --target=api
```

輸出格式：
```
{專案名}：⚠️ 偵測到舊格式殘留
  - functional.md 仍存在但未遷移 → 建議執行 /migrate-kb {專案} --target=reqs
```

三項皆未命中 → 不輸出此區塊。

---

## 檔案歸屬一致性檢查（內容類型與所在路徑是否相符）

掃描以下專案目錄，確認檔案的標頭 ID 前綴與其所在目錄相符（偵測誤放檔案）。排除清單與 `schema.md` 2-2/2-5/2-6/2-7 的排除規則一致：

| 目錄 | 預期 ID 前綴 | 排除檔案 |
|------|------------|----------|
| `01-requirements/_pending/` | `PENDING-` | `_index.md` |
| `01-requirements/_inferred/` | `INF-` 或 `GAP-` | `_index.md` |
| `04-decisions/` | `ADR-` | `ADR-index.md`、`ADR-000-template.md` |
| `06-qa-testing/bugs/` | `BUG-` | （無） |

對每個非排除檔案：
```
[ ] 檔案標頭的 ID 前綴與所在目錄的預期前綴相符
```
不符 → 🟡 警告：「{檔案路徑} 的內容類型（{實際 ID}）與所在目錄不符，疑似誤放，建議移至正確目錄」

輸出格式：
```
{專案名}：⚠️ 發現 {N} 個疑似誤放檔案
  - {路徑}：標頭為 {實際ID}，但目錄預期為 {預期前綴}
```

未命中 → 不輸出此區塊。

---

## 非預期檔案掃描（白名單比對，僅供提醒，非健康度扣分項）

專案目錄下的檔案分三類，皆屬合法，**不算「未分類」**：
1. `/project-init` 建立的固定檔案（見 `.claude/commands/project-init.md` 步驟 3 全列表，含各 `README.md`/`index.md`）
2. 已知 ID 前綴命名慣例：`PENDING-` / `INF-` / `GAP-` / `BUG-` / `ADR-`
3. **依名稱動態建立、檔名本身就不固定**的合法慣例：見 `{KB_ROOT}/.claude/protocols/structure-map.md` 結構總覽中列出的動態命名項目（`functional/{m}.md`、`system-design/{c}.md`、`api-contracts/{g}.md`、`_legacy-analysis.md`、`collab/{initials}.md` 等）；新增慣例時只在 structure-map.md 增改，此處不重複列舉

```
[ ] 列出專案目錄下，三類皆不符的額外檔案或資料夾
```

只有三類都不符的項目才視為「未分類」，這類項目可能是合理的擴充（例如工程師自行補充的筆記），不代表錯誤，因此**不計入健康度評分**，僅供確認。

輸出格式：
```
ℹ️ {專案名} 發現 {N} 個未分類項目（僅供確認，非錯誤）：
  - {路徑}
```

完全比對標準結構 → 不輸出此區塊。

---

## Wiki 知識層結構驗證（若 wiki/ 存在）

確認以下 wiki 層基礎架構存在：

```
必要（wiki 層已啟動的前提）：
  [ ] wiki/hot/ 至少 1 個 {initials}.md
  [ ] wiki/index.md
  [ ] wiki/log.md

知識層（有內容時應存在）：
  [ ] wiki/concepts/_index.md
  [ ] wiki/entities/_index.md
  [ ] wiki/sources/_index.md
  [ ] wiki/questions/_index.md
  [ ] wiki/overview.md

Obsidian 整合（選配）：
  [ ] .obsidian/snippets/vault-colors.css
  [ ] .raw/ 資料夾（原始文件存放區）
  [ ] hooks/hooks.json（session 自動化）
```

若 wiki/ 不存在或為空 → 略過此段，只做工程層檢查。

→ 完成後讀取 `_health-check/schema.md`（若完整診斷模式）
