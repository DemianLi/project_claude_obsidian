# Phase 1：讀取背景

依序讀取以下檔案，建立分析基礎：

```
1. projects/{專案}/02-architecture/arch-index.md          → 元件地圖，再讀相關 system-design/{component}.md
2. projects/{專案}/02-architecture/api-contracts/index.md → API 群組索引，再讀相關 {module}.md
3. projects/{專案}/02-architecture/_legacy-analysis.md     → 現有 DB 結構（若有）
4. projects/{專案}/01-requirements/functional-index.md     → 模組索引，再讀相關 functional/{module}.md 取得所有已確認需求
5. projects/{專案}/04-decisions/                            → 已有的技術決策（ADR）
```

若 `api-contracts/index.md` 或 `_legacy-analysis.md` 不存在，跳過並標記「無對應資訊」。

讀取完成後，在內部建立分析摘要：
- 現有 table 清單（若有 legacy-analysis）
- 現有 API 端點清單
- 現有 REQ 清單（已確認的）
- 現有 ADR 決策清單

→ 完成後讀取 `_impact/analyze.md`
