# Phase 1：結構完整性檢查

對每個進行中專案（或指定專案），驗證必要檔案是否存在：

```
必要檔案（10 個，各佔 10 分）：
  [ ] 00-overview.md
  [ ] 01-requirements/functional.md
  [ ] 01-requirements/scope.md
  [ ] 01-requirements/_pending.md
  [ ] 01-requirements/_inferred.md
  [ ] 02-architecture/system-design.md
  [ ] 03-client-context/existing-system.md
  [ ] 03-client-context/domain-knowledge.md
  [ ] 03-client-context/stakeholders.md
  [ ] 06-qa-testing/bugs.md

加分項（完整度更高但非必要）：
  [ ] 02-architecture/api-contracts.md
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

→ 完成後讀取 `_health-check/schema.md`（若完整診斷模式）
