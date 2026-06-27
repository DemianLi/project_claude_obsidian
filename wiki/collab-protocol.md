---
type: collab-protocol
updated: 2026-06-27
---

# 多工程師協作協議

> 當專案有 2 人以上共同維護知識庫時，依此文件操作。
> 核心設計：**檔案層級零衝突**（每個知識單元各自一檔）+ **REQ 層級軟性鎖定**（自動偵測，不需人工審核）。
> 不採用 git branch / PR 審核工作流——知識庫版控由 **Obsidian git 插件自動管理**，直接寫入即可，靠檔案拆分本身避免衝突，不靠流程把關。

---

## 一、檔案所有權矩陣

| 檔案 | 所有權 | 衝突風險 | 操作規則 |
|------|--------|----------|----------|
| `01-requirements/functional/{module}.md` | 模組層級共用 | 🟡 中 | 寫入前先看 `.claude/collab/*.md` 是否有人鎖定該 REQ（見二） |
| `01-requirements/scope.md` | 共用 | 🟡 中 | 異動前先 `git pull` 同步 |
| `01-requirements/_pending/{ID}.md` | **各自一檔** | 🟢 低 | 新增各建新檔，零衝突；`/reconcile` 合併重複，不手動刪除 |
| `01-requirements/_inferred/{ID}.md` | **各自一檔** | 🟢 低 | 同 `_pending/` |
| `06-qa-testing/bugs/{BUG-ID}.md` | **各自一檔** | 🟢 低 | 同上 |
| `04-decisions/ADR-*.md` | 全體討論，建立者記錄 | 🟡 中 | 建立前先在團隊內討論，建立者在 ADR 中記錄「參與討論者」 |
| `05-dev-notes/YYYY-MM-DD-*.md` | **各自建立，不交叉** | 🟢 低 | 每人用自己的日期+主題命名，自然無衝突 |
| `wiki/hot/{縮寫}.md` | **各自所有** | 🟢 低 | 每人各自一檔，`/save` 只替換自己的，不會互相覆寫 |
| `wiki/log.md` | 共用，**Append-only** | 🟢 低 | 只 append，git merge 幾乎不會衝突 |
| `wiki/index.md` | 共用 | 🟡 中 | 狀態變更前先 `git pull` 同步 |
| `02-architecture/*.md` | 共用 | 🔴 高 | 異動前先溝通，這塊還沒有自動衝突偵測 |
| `03-client-context/*.md` | 共用 | 🟡 中 | 以 `/ingest` 走正式流程，不直接手動覆寫 |
| `knowledge/patterns/PAT-*.md`、`lessons-learned/LESSON-*.md`、`tech-stack/{slug}.md` | **各自一檔** | 🟢 低 | 新增各建新檔；同一條目的更新才需要互相確認 |
| `.claude/collab/{縮寫}.md` | **各自所有** | 🟢 低 | 只寫自己的鎖定狀態，見二 |

---

## 二、REQ 鎖定機制（自動，不需人工審核）

### 開始實作前

BEFORE CODING Stage 3.5 會自動執行（`{KB_ROOT}/.claude/impl/_collab/check.md`）：
1. 讀取 `projects/{專案}/.claude/collab/*.md`，合併所有工程師的 `active_work` 鎖定清單
2. 比對目標 REQ，無衝突直接繼續
3. 有衝突 → 顯示鎖定工程師/日期，要求確認是否仍要繼續（Y 繼續但建議先溝通／N 停止）

不需要手動 `git pull` 看 `hot/*.md` 猜誰在做什麼——這一步是自動的。

### 結束工作後

`/save` 會自動執行（`_collab/update.md`）：
1. 讀自己的 `collab/{縮寫}.md`，詢問本次實作的 REQ 是否要鎖定／已完成的 REQ 是否要解鎖
2. **只寫入自己的檔案**，不碰其他工程師的 `collab/{縮寫}.md`

### 無 collab/ 資料夾時

整個機制自動跳過，視為單人專案。第二位工程師加入時執行 `/project-init` 詢問成員縮寫，建立 `collab/{initials}.md`。

---

## 三、合併衝突處理（萬一還是撞到）

| 衝突類型 | 解決方式 |
|----------|----------|
| `functional/{module}.md` 中同一條需求的衝突 | 手動裁決，以較新日期版本為準，記錄「為何以此版本為準」 |
| `_pending/`、`_inferred/`、`bugs/` 條目重複 | 執行 `/reconcile` 合併，不手動刪除（各自獨立檔案，本來就很少真的衝突） |
| `wiki/log.md` 衝突 | 兩段都保留（append-only 的天然特性） |
| `knowledge/` 同一條目衝突 | 兩版本都保留，等下次 `/self-improve` 合併 |

---

## 四、Claude 的行為調整

在多工程師環境下，Claude 在以下情況會特別謹慎：

| 情況 | Claude 的行為 |
|------|--------------|
| BEFORE CODING 命中 REQ 鎖定衝突 | 見二，自動顯示鎖定資訊並要求確認 |
| 要建立 ADR | 提醒：「ADR 影響全體工程師，建議先在團隊中討論」 |
| `/reconcile` 發現疑似衝突條目 | 標記「可能來自不同工程師的不同觀察，建議同步確認後再合併」 |
| 發現 `wiki/hot/*.md` 顯示多人最近有活動 | 提示：「近期有 {N} 位工程師工作記錄，建議先 `git pull` 再繼續」 |

---

## 五、知識庫健康維護分工

| 任務 | 負責人 | 頻率 |
|------|--------|------|
| 執行 `/reconcile` 整理 pending/inferred | 任一工程師 | 每 2 週 |
| 執行 `/self-improve` 提煉模式與教訓 | 任一工程師 | 每完成一個功能模組 |
| 更新 `wiki/index.md` 專案狀態 | 任一工程師 | 里程碑達成時 |
| 審核 `knowledge/patterns/` 新增提案 | 全體 | 有新 pattern 提案時 |

---

*此文件應在第二位工程師加入專案、執行 `/project-init` 建立 `collab/` 結構時主動提示閱讀。*
