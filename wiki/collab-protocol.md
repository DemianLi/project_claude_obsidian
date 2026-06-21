---
type: collab-protocol
updated: 2026-06-21
---

# 多工程師協作協議

> 當專案有 2 人以上共同維護知識庫時，依此文件的規則操作，
> 避免相互覆寫造成資料遺失或衝突。
>
> 工具前提：以 **Git** 作為知識庫的同步與版本控制機制。
> 若尚未初始化 Git：`git init && git add . && git commit -m "init knowledge base"`

---

## 一、檔案所有權矩陣

不同檔案的衝突風險不同，依照以下規則操作：

| 檔案 | 所有權 | 衝突風險 | 操作規則 |
|------|--------|----------|----------|
| `01-requirements/functional.md` | **專案主導（1人）** | 🔴 高 | 其他人以 PR/Branch 提交修改，主導人審核後合併 |
| `01-requirements/scope.md` | **專案主導（1人）** | 🔴 高 | 同上 |
| `01-requirements/_pending.md` | 共用，**Append-only** | 🟡 中 | 每人只新增，不修改他人的條目；新條目加上 `(作者縮寫)` 標記 |
| `01-requirements/_inferred.md` | 共用，**Append-only** | 🟡 中 | 同 _pending.md |
| `04-decisions/ADR-*.md` | **全體討論，主導人建立** | 🟡 中 | ADR 在 Slack/email 中討論後，才建立文件；建立者在 ADR 中記錄「參與討論者」 |
| `05-dev-notes/YYYY-MM-DD-*.md` | **各自建立，不交叉** | 🟢 低 | 每人用自己的日期+主題命名，自然無衝突 |
| `wiki/log.md` | 共用，**Append-only** | 🟢 低 | 只 append，Git merge 幾乎不會衝突 |
| `wiki/hot.md` | **最後工作者更新** | 🟡 中 | 每次 `/save` 完整替換；若多人同天工作，各自追加一個 "## 工程師B 的更新" section |
| `wiki/index.md` | 共用 | 🟡 中 | 狀態變更前先 `git pull` 同步 |
| `02-architecture/*.md` | **主架構師主導** | 🔴 高 | 修改前開 branch，討論後合併 |
| `03-client-context/*.md` | 共用 | 🟡 中 | 以 `/ingest` 走正式流程，不直接手動覆寫 |
| `knowledge/**/*.md` | 共用 | 🟡 中 | 各自 append，衝突時保留雙方版本再合併 |

---

## 二、分支工作流程

### 日常開發（低風險改動）

```bash
# 每次開始工作前
git pull origin main

# 做完 /save
git add .
git commit -m "[專案名] [YYYY-MM-DD] [一句話摘要]"
git push origin main
```

### 修改 functional.md 或 architecture/（高風險改動）

```bash
# 建立 feature branch
git checkout -b feat/REQ-F001-login-flow

# ... 修改 functional.md ...

# 提交並開 PR
git push origin feat/REQ-F001-login-flow
# → 在 GitHub/GitLab 開 Pull Request，指定主導工程師 review
```

### 合併衝突解決規則

| 衝突類型 | 解決方式 |
|----------|----------|
| `functional.md` 中同一條需求的衝突 | 主導工程師手動裁決，以較新日期版本為準，並記錄「為何以此版本為準」 |
| `_pending.md` 條目重複 | 執行 `/reconcile` 合併，不手動刪除 |
| `wiki/hot.md` 衝突 | 保留雙方內容，各自在對應「工程師」section 下；下次 /save 時整合 |
| `wiki/log.md` 衝突 | 兩段都保留（append-only 的天然特性） |
| `knowledge/patterns/` 或 `lessons-learned/` 衝突 | 兩版本都保留，等下次 `/self-improve` 合併 |

---

## 三、協同工作約定

### 開始工作前（必做）

```bash
git pull origin main
```

讀取 `wiki/hot.md` → 了解其他工程師最近的工作狀態。
若看到其他人正在處理相同的需求，**先溝通再動**。

### 需求鎖定機制

當你開始實作某條 REQ 時，在 `functional.md` 的對應條目加上：

```markdown
**實作中**：🔒 {你的名字縮寫}（{YYYY-MM-DD}）
```

實作完成後移除此標記。這個軟性鎖定讓其他工程師知道「這條有人在做」。

### `/save` 後的通知

完成 `/save` 並 push 後，在團隊頻道簡短通報：
```
[專案名] 已更新 hot.md — [一句話說明本次做了什麼]
```

---

## 四、Claude 的行為調整

在多工程師環境下，Claude 在以下情況會特別謹慎：

| 情況 | Claude 的行為 |
|------|--------------|
| 要寫入 `functional.md` | 先確認：「此需求是否已由其他工程師鎖定（🔒）？」 |
| 發現 hot.md 顯示多人最近有活動 | 提示：「近期有 {N} 位工程師工作記錄，建議先 `git pull` 再繼續」 |
| 要建立 ADR | 提醒：「ADR 影響全體工程師，建議在建立前先在團隊中討論」 |
| `/reconcile` 發現疑似衝突條目 | 標記「可能來自不同工程師的不同觀察，建議同步確認後再合併」 |

---

## 五、角色分工建議

這是建議，非強制；可根據團隊習慣調整：

| 角色 | 負責 |
|------|------|
| **專案主導（Project Lead）** | 維護 `functional.md`、`scope.md`、`02-architecture/`；審核 PR；發起 ADR |
| **實作工程師** | 建立 `05-dev-notes/`；更新 `_pending.md`（發現問題時）；執行 `/save` |
| **任何人** | 執行 `/query`、`/research`、`/reverse-engineer`（唯讀操作，不影響協作） |

---

## 六、知識庫健康維護分工

| 任務 | 負責人 | 頻率 |
|------|--------|------|
| 執行 `/reconcile` 整理 pending/inferred | 專案主導 | 每 2 週 |
| 執行 `/self-improve` 提煉模式與教訓 | 任一工程師 | 每完成一個功能模組 |
| 更新 `wiki/index.md` 專案狀態 | 專案主導 | 里程碑達成時 |
| 審核 `knowledge/patterns/` 新增提案 | 專案主導 | 有新 pattern 提案時 |

---

*此文件應在 `/project-init` 時自動提示建立，或在第二位工程師加入專案時主動建立。*
