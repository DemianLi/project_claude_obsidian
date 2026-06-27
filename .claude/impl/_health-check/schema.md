# Phase 2：格式合規性驗證（Schema Check）

讀取 `knowledge/_schemas/` 中的 schema 定義，驗證各檔案格式。

## 2-1. functional/{module}.md — REQ 格式驗證（依據 req.md）
```
對每條 REQ 檢查：
  [ ] 標頭格式：## REQ-F{三位數}：{標題}
  [ ] **狀態** 欄位存在且值在有效列表中
  [ ] **確認日期** 格式為 YYYY-MM-DD
  [ ] **來源文件** 欄位存在（非空）
  [ ] **合約版本** 欄位存在
  [ ] ### 描述 section 存在且非空
  [ ] ### 驗收條件 至少 1 條 `- [ ]` 項目
  [ ] ID 在此檔案中唯一（不重複）
```

## 2-2. 04-decisions/*.md — ADR 格式驗證（依據 adr.md）
```
對每份 ADR 檢查：
  [ ] frontmatter 存在（有 id, status, date）
  [ ] status 在有效值列表中
  [ ] ## 背景 section 存在
  [ ] ## 決策 section 存在
  [ ] ## 後果 section 存在
  [ ] 若 status: superseded → superseded_by 必須存在
```

## 2-3. knowledge/patterns/*.md — PAT 格式驗證（依據 pat.md）
```
對每個 PAT 條目檢查：
  [ ] tags 欄位存在（至少 1 個）
  [ ] status 欄位存在且值有效
  [ ] validated/experimental → projects 非空
  [ ] 有「適用情境」說明
  [ ] 有「注意事項」（至少 1 條）
```

## 2-4. knowledge/lessons-learned/*.md — LESSON 格式驗證（依據 lesson.md）
```
對每條 LESSON 檢查：
  [ ] tags 欄位存在
  [ ] phase 欄位存在且值有效
  [ ] root_cause 欄位存在且值有效
  [ ] 「預防方式」欄位存在且非空
  [ ] 「偵測信號」欄位存在且非空
  [ ] 「是否已納入系統守衛」已填
```

問題分類：
- 🔴 嚴重：缺少驗收條件 / ADR 缺少後果
- 🟡 警告：缺少 tags / 欄位格式不符

→ 完成後讀取 `_health-check/stale.md`（若完整診斷模式）
