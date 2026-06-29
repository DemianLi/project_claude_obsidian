---
type: collab-protocol
updated: 2026-06-27
---

# 多工程師協作協議

> 當專案有 2 人以上共同維護知識庫時，依此文件操作。
> 核心設計：**檔案層級零衝突**（每個知識單元各自一檔）+ **REQ / 元件 / API 群組軟性鎖定**（自動偵測，不需人工審核）+ **整份共用文件靠提醒與記錄**（無法分割成獨立記錄的檔案）。
> 不採用 git branch / PR 審核工作流——知識庫版控由 **Obsidian git 插件自動管理**，直接寫入即可，靠檔案拆分本身避免衝突，不靠流程把關。

---

## 一、檔案所有權矩陣

| 檔案 | 所有權 | 衝突風險 | 操作規則 |
|------|--------|----------|----------|
| `01-requirements/functional/{module}.md` | 模組層級共用 | 🟡 中 | 寫入前先看 `collab/*.md` 是否有人鎖定該 REQ（見二） |
| `01-requirements/scope.md` | 共用，整份文件 | 🟡 中 | 不適用鎖定，靠「先確認最新版本 + 異動後留 log」（見三） |
| `01-requirements/_pending/{ID}.md` | **各自一檔** | 🟢 低 | 新增各建新檔，零衝突；`/reconcile` 合併重複，不手動刪除 |
| `01-requirements/_inferred/{ID}.md` | **各自一檔** | 🟢 低 | 同 `_pending/` |
| `06-qa-testing/bugs/{BUG-ID}.md` | **各自一檔** | 🟢 低 | 同上 |
| `04-decisions/ADR-*.md` | 各自一檔（決策內容）+ `ADR-index.md` 共用（薄索引） | 🟡 中 | 決策內容本身各自一檔零衝突；建立前先在團隊內討論，建立者在 ADR 中記錄「參與討論者」（見四） |
| `05-dev-notes/YYYY-MM-DD-*.md` | **各自建立，不交叉** | 🟢 低 | 每人用自己的日期+主題命名，自然無衝突 |
| `wiki/hot/{縮寫}.md` | **各自所有** | 🟢 低 | 每人各自一檔，`/save` 只替換自己的，不會互相覆寫 |
| `wiki/log.md` | 共用，**Append-only** | 🟢 低 | 只 append，git merge 幾乎不會衝突 |
| `wiki/index.md` | 共用，整份文件 | 🟡 中 | 不適用鎖定，靠「先確認最新版本 + 異動後留 log」（見三） |
| `02-architecture/system-design/{component}.md`、`api-contracts/{group}.md` | 元件/群組層級共用 | 🟡 中（原 🔴，已補上鎖定機制） | 寫入前先看 `collab/*.md` 是否有人鎖定該元件/群組（機制同 REQ，見二） |
| `02-architecture/arch-index.md`、`api-contracts/index.md` | 共用，薄索引 | 🟢 低 | 由指令自動維護，單次寫入動作短暫，實質衝突窗口很小 |
| `03-client-context/*.md` | 共用，整份文件 | 🟡 中 | 以 `/ingest` 走正式流程為主；若手動編輯，適用「先確認最新版本 + 異動後留 log」（見三） |
| `knowledge/patterns/PAT-*.md`、`lessons-learned/LESSON-*.md`、`tech-stack/{slug}.md` | **各自一檔** | 🟢 低 | 新增各建新檔；同一條目的更新才需要互相確認 |
| `collab/{縮寫}.md` | **各自所有** | 🟢 低 | 只寫自己的鎖定狀態，見二 |

---

## 二、鎖定機制（REQ + 架構元件 + API 群組，自動，不需人工審核）

適用對象：能拆成獨立記錄、有明確「誰在做」邊界的工作單元——`functional/{module}.md` 的 REQ、`system-design/{component}.md` 的元件、`api-contracts/{group}.md` 的 API 群組。三者共用同一套機制，只是鎖定鍵的「類型」不同。

### 開始實作前

BEFORE CODING Stage 3 會自動執行（`{KB_ROOT}/.claude/impl/_collab/check.md`）：
1. 讀取 `projects/{專案}/collab/*.md`，合併所有工程師的 `active_work` 鎖定清單
2. 識別本次任務涉及的目標——REQ（可能沒有，例如純架構任務）、元件、API 群組，三類任一命中即比對
3. 無衝突直接繼續
4. 有衝突 → 顯示鎖定工程師/日期/類型，並標示鎖定是否已超過 14 天未更新（⏰ 可能已過期，僅為提示不會自動解除），要求確認是否仍要繼續（Y 繼續但建議先溝通／N 停止）

**純架構任務一樣會被檢查**：即使沒有對應 REQ，只要任務涉及修改 `02-architecture/` 下的元件或 API 群組設計，check.md 會直接識別元件/群組目標，不需要先找到 REQ 才觸發。

不需要手動 `git pull` 看 `hot/*.md` 猜誰在做什麼——這一步是自動的。

### 結束工作後

`/save` 會自動執行（`_collab/update.md`）：
1. 讀自己的 `collab/{縮寫}.md`，詢問本次涉及的 REQ／元件／API 群組是否要鎖定、已完成的項目是否要解鎖
2. **只寫入自己的檔案**，不碰其他工程師的 `collab/{縮寫}.md`

### 無 collab/ 資料夾時

整個機制自動跳過，視為單人專案。第二位工程師加入時執行 `/project-init` 詢問成員縮寫，建立 `collab/{initials}.md`。

### 機制的已知邊界

鎖定的可靠度取決於每個人 collab/ 內容的新鮮度——若工程師 A 鎖定了某元件，但工程師 B 的本機知識庫還沒拉到 A 這次的更新，B 的 BEFORE CODING 就看不到這個鎖定。這套機制只負責「資料新鮮時正確偵測」，不負責「確保資料一定新鮮」；後者取決於 Obsidian git 插件的自動同步時機，是獨立於這套機制的風險。鎖定的「⏰ 可能已過期」提示同樣只在 BEFORE CODING 比對時計算（無背景常駐程序），且僅供參考，不會自動刪除其他工程師的鎖定條目——真正解鎖仍由鎖定者自己在下次 `/save` 時處理。

---

## 三、整份共用文件的處理規則（不適合鎖定的檔案）

以下檔案是單一整份文件，不像 REQ／元件／API 群組那樣能拆成獨立記錄，不適用鎖定機制：

- `01-requirements/scope.md`
- `wiki/index.md`
- `03-client-context/stakeholders.md`、`existing-system.md`、`domain-knowledge.md`

**處理方式（行為準則，非技術鎖定）**：
1. 異動前，Claude 主動提示：「{檔案} 是團隊共用檔案，建議先確認本機知識庫是最新版本」
2. 異動後，在 `wiki/log.md` append 一筆：「{日期} {縮寫} 異動了 {檔案}：{摘要}」，讓其他工程師下次讀 log 時能注意到
3. 若發現自己即將覆寫的內容跟讀取時的版本不同（疑似其他人剛異動過），停止並回報差異，不靜默覆寫

這類檔案編輯頻率低（多在專案初期或里程碑時異動），「提醒 + 記錄」已足夠；真正撞期時靠下面的合併衝突處理。

---

## 四、合併衝突處理（萬一還是撞到）

| 衝突類型 | 解決方式 |
|----------|----------|
| `functional/{module}.md` 中同一條需求的衝突 | 手動裁決，以較新日期版本為準，記錄「為何以此版本為準」 |
| `system-design/{component}.md`、`api-contracts/{group}.md` 中同一元件/群組的衝突 | 同上，手動裁決、以較新日期版本為準並記錄理由 |
| `_pending/`、`_inferred/`、`bugs/` 條目重複 | 執行 `/reconcile` 合併，不手動刪除（各自獨立檔案，本來就很少真的衝突） |
| `wiki/log.md` 衝突 | 兩段都保留（append-only 的天然特性） |
| `knowledge/` 同一條目衝突 | 兩版本都保留，等下次 `/self-improve` 合併 |

---

## 五、Claude 的行為調整

在多工程師環境下，Claude 在以下情況會特別謹慎：

| 情況 | Claude 的行為 |
|------|--------------|
| BEFORE CODING 命中鎖定衝突（REQ／元件／API 群組） | 見二，自動顯示鎖定資訊並要求確認 |
| 要異動 `scope.md`、`wiki/index.md`、`03-client-context/*.md` | 見三，先提示確認最新版本，異動後留 log |
| 要建立 ADR | 提醒：「ADR 影響全體工程師，建議先在團隊中討論」 |
| `/reconcile` 發現疑似衝突條目 | 標記「可能來自不同工程師的不同觀察，建議同步確認後再合併」 |
| 發現 `wiki/hot/*.md` 顯示多人最近有活動 | 提示：「近期有 {N} 位工程師工作記錄，建議先 `git pull` 再繼續」 |

---

## 六、知識庫健康維護分工

| 任務 | 負責人 | 頻率 |
|------|--------|------|
| 執行 `/reconcile` 整理 pending/inferred | 任一工程師 | 每 2 週 |
| 執行 `/self-improve` 提煉模式與教訓 | 任一工程師 | 每完成一個功能模組 |
| 更新 `wiki/index.md` 專案狀態 | 任一工程師 | 里程碑達成時 |
| 審核 `knowledge/patterns/` 新增提案 | 全體 | 有新 pattern 提案時 |

---

*此文件應在第二位工程師加入專案、執行 `/project-init` 建立 `collab/` 結構時主動提示閱讀。*
