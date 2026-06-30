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
排除 ADR-index.md（薄索引，非個別決策）與 ADR-000-template.md（建立新 ADR 時複製的空白範本，非實際決策）。
對每份 ADR 檢查：
  [ ] frontmatter 存在（有 id, status, date）
  [ ] status 在有效值列表中
  [ ] ## 背景 section 存在
  [ ] ## 決策 section 存在
  [ ] ## 後果 section 存在
  [ ] 若 status: superseded → superseded_by 必須存在
  [ ] id 格式為 ADR-{三位數字}
  [ ] 檔案僅含一個 # ADR- 標頭（一檔一條目）
```

## 2-3. knowledge/patterns/*.md — PAT 格式驗證（依據 pat.md）
```
排除 index.md（薄索引，非個別條目，格式完全不同）。
對每個 PAT 條目檢查：
  [ ] tags 欄位存在（至少 1 個）
  [ ] status 欄位存在且值有效
  [ ] validated/experimental → projects 非空
  [ ] 有「適用情境」說明
  [ ] 有「注意事項」（至少 1 條）
  [ ] ID 格式為 PAT-{CATEGORY}-{三位數字}，CATEGORY 在有效分類列表中
  [ ] 檔案僅含一個 # PAT- 標頭（一檔一條目）
```

## 2-4. knowledge/lessons-learned/*.md — LESSON 格式驗證（依據 lesson.md）
```
排除 index.md（薄索引，非個別條目，格式完全不同）。
對每條 LESSON 檢查：
  [ ] tags 欄位存在
  [ ] phase 欄位存在且值有效
  [ ] root_cause 欄位存在且值有效
  [ ] 「預防方式」欄位存在且非空
  [ ] 「偵測信號」欄位存在且非空
  [ ] 「是否已納入系統守衛」已填
  [ ] ID 格式為 LESSON-{三位數字}
  [ ] 檔案僅含一個 # LESSON- 標頭（一檔一條目）
```

## 2-5. _pending/{ID}.md — PENDING 格式驗證（依據 pending.md）
```
排除 _index.md（薄索引，非個別條目，格式完全不同）。
對每條 PENDING 檢查：
  [ ] 原文 / 來源 / 問題 欄位存在
  [ ] 優先級 欄位存在且值在有效列表中
  [ ] 阻塞性 欄位存在；若為「是」，須附說明文字（不可空白）
  [ ] 建議問甲方 區塊存在且非空
  [ ] 狀態 欄位存在且值在有效列表中
  [ ] 建立日期 格式為 YYYY-MM-DD
  [ ] ID 在此專案中唯一（不重複）
  [ ] 標頭 ID 格式為 PENDING-{三位數字}
  [ ] 檔案僅含一個 # PENDING- 標頭（一檔一條目）
```

## 2-6. _inferred/{ID}.md — INF/GAP 格式驗證（依據 inferred.md）
```
排除 _index.md（薄索引，非個別條目，格式完全不同）。
對每條 INF-XXX 檢查：
  [ ] 標頭 / 推測依據 / 信心度 / 需驗證 欄位存在
  [ ] 信心度值在有效列表中（🟢/🟡/🔴）
  [ ] 標頭 ID 格式為 INF-{數字}

對每條 GAP-XXX 檢查：
  [ ] 標頭 / 類型 / 現象 / 影響 / 建議問甲方 欄位存在
  [ ] 類型值在有效列表中（⚡/🗃️/🔀/🔘/🔢）
  [ ] 標頭 ID 格式為 GAP-{數字}

對每個檔案檢查：
  [ ] 僅含一個 INF- 或 GAP- 標頭（一檔一條目）

> 狀態、更新紀錄等屬選用擴充欄位，`/reverse-engineer` 預設不寫入，缺少不算不健康。
```

## 2-7. bugs/{BUG-ID}.md — BUG 格式驗證（依據 bug.md）
```
對每個 BUG 檢查：
  [ ] 狀態 / 嚴重度 / 根因類型 / 描述 / 發現日期 欄位存在
  [ ] 狀態、嚴重度、根因類型值皆在有效列表中
  [ ] 預期結果 / 實際結果 欄位皆存在
  [ ] 發現日期格式為 YYYY-MM-DD
  [ ] 狀態為「✅ 已關閉」時，修復方案與修復日期不可為「—」（資料不一致）
  [ ] ID 在此專案中唯一（不重複）
  [ ] 標頭 ID 格式為 BUG-{三位數字}
  [ ] 檔案僅含一個 # {BUG-ID} 標頭（一檔一條目）
```

## 2-8. collab/{initials}.md — 鎖定格式驗證（依據 collab.md）
```
對每份 collab 檔案檢查：
  [ ] frontmatter engineer / updated 欄位存在
  [ ] frontmatter engineer 與檔名一致
  [ ] active_work 表格每列「類型」值在有效列表中（REQ/元件/API群組；「（無）」佔位列不檢查）
  [ ] active_work 表格每列「鎖定日期」格式為 YYYY-MM-DD（佔位列不檢查）
```

問題分類：
- 🔴 嚴重：缺少驗收條件 / ADR 缺少後果 / BUG 已關閉但無修復方案 / 同一檔案含多個條目（違反一檔一條目）
- 🟡 警告：缺少 tags / 欄位格式不符 / PENDING 阻塞性「是」但無說明 / ID 命名格式不符規則

→ 完成後讀取 `_health-check/stale.md`（若完整診斷模式）
