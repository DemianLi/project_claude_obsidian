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
