# Phase 2：更新 wiki + 維護薄索引（多數步驟自動執行，Step 9 內容性缺陷會詢問）

## Step 4：更新 `{KB_ROOT}/wiki/hot/{engineer}.md`（完整替換自己的檔案）

工程師縮寫從 `{KB_ROOT}/projects/{名稱}/collab/{initials}.md` 讀取；若無 collab 資料則詢問縮寫或預設 `default`。
每位工程師只替換自己的檔案，其他人的 hot 檔案不動。

```markdown
## 🔄 最近工作（{日期}）｜{engineer}

**活躍專案**：{專案名}
**上次工作**：{YYYY-MM-DD}

### 本次完成
- {完成項目}

### 進行中
- {還在做的}

### 待辦（下次繼續）
- {未完成}

### 重要決策
- {記錄重要決策}

### 注意事項
- {下次需要記住的事}
```

## Step 5：Append `{KB_ROOT}/wiki/log.md`

```
### [{日期}] {專案} — {一句話摘要}
- {完成項目}
- {重要決策}
- {遺留問題}
```

## Step 8：維護索引與 Quick Context（自動執行，不需確認）

⚠️ 以下所有路徑均在 `{KB_ROOT}/` 下，不寫入 `{CODE_ROOT}/`。

| 更新目標 | 更新內容 | 條件 |
|----------|---------|------|
| `{KB_ROOT}/projects/{名稱}/01-requirements/functional-index.md` | 更新需求數統計、模組狀態摘要 | 本次有新增或修改 REQ |
| `{KB_ROOT}/projects/{名稱}/04-decisions/ADR-index.md` | Append 新 ADR 一行摘要 | 本次建立新 ADR |
| `{KB_ROOT}/projects/{名稱}/05-dev-notes/_index.md` | Append 今日 session 一行摘要（日期/REQ/工時/標籤） | 本次有 dev-notes |
| `{KB_ROOT}/projects/{名稱}/06-qa-testing/bugs-active.md` | 移除已關閉 bug；更新統計摘要 | 本次有關閉 bug |
| `{KB_ROOT}/projects/{名稱}/01-requirements/_pending/_index.md` | 更新 QUICK CONTEXT 頭（阻塞數/總數） | 本次有新增或解決 PENDING |
| `{KB_ROOT}/projects/{名稱}/01-requirements/_inferred/_index.md` | 更新 QUICK CONTEXT 頭（高風險數/GAP 數） | 本次有新增或升格 INF/GAP |
| 各文件的 `## 📌 Quick Context` | 更新本次修改過文件的 Quick Context 區塊 | 文件內容有異動 |

Quick Context 沒有統一範本，各檔案類型欄位不同（依內容性質而定，例如 functional module 摘要已確認/待確認數，system-design 摘要職責/邊界）：直接沿用該檔案現有的 Quick Context 欄位結構，覆寫為本次 session 後的最新數值，不套用固定欄位名稱。

## Step 9：輕量 schema 自檢（只查本次異動的 REQ/ADR 檔案）

只針對本次 session 有新增或修改的 `functional/{module}.md`（REQ）與 `04-decisions/ADR-*.md`（ADR）檔案，依 `knowledge/_schemas/req.md`／`adr.md` 的必填欄位規則檢查。不做全庫掃描——那是 `/health-check` 的職責，這裡只把關「剛寫的東西」。

**結構性缺陷 → 直接修復，不需確認**（系統自己就能判斷的事實）：
- 缺少 `updated`（檔案最後異動日期）欄位 → 補今天日期
- 既有日期欄位格式不是 YYYY-MM-DD → 修正格式（不改變欄位代表的事實，只修格式）

**內容性缺陷 → 列出並詢問，不可靜默編造內容**（這些是外部事實，Claude 不能代替甲方或工程師判斷）：
- 缺少 `確認日期`（甲方何時確認，是外部事實，不可用今天日期頂替）
- 缺少驗收條件 / 描述為空
- 狀態值不在有效列表中
- ID 與同檔案其他項目重複

```
⚠️ 本次異動的檔案發現 {N} 項格式問題：
  1. {檔案}：{問題描述}
是否現在補上，或先記錄待辦稍後再補？
```

若本次無異動 REQ/ADR 檔案 → 跳過此步驟。

→ 完成後讀取 `_save/report.md`
