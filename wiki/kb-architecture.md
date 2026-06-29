# ADR-KB-001：知識庫深度架構優化

**狀態**：Accepted  
**日期**：2026-06-21  
**適用範圍**：整套軟體工程知識庫協作系統

---

## 背景

知識庫運行至今（累計覆蓋 21 個使用場景），已能處理需求管理、變更控制、交付文件等核心流程。但隨著專案數量和知識條目增加，以下問題開始浮現：

1. **AI 導航效率下降**：BEFORE CODING 需讀 10+ 個檔案，即使任務只涉及其中 5%
2. **無法自我驗證**：知識庫沒有驗證機制，格式錯誤會靜默傳遞而非立即報錯
3. **淺模組問題**：`knowledge/patterns/index.md`、`lessons-learned/index.md` 等單一大檔案隨著條目增加成為難以查詢的巨型文件
4. **指令無前置條件宣告**：指令假設所有依賴都存在，在未初始化的專案上運行會產生難以理解的失敗

這份 ADR 記錄所有識別到的架構摩擦點，以及如何透過「將淺模組深化」來解決。

---

## 識別到的架構摩擦點

### F1：CLAUDE.md 是 God Module（嚴重度：🔴 高）

**問題描述：**

CLAUDE.md 同時承擔了 7 個職責：
- 角色定義
- 4 個生命週期協議（SESSION START / BEFORE CODING / AFTER TASK / SAVE SESSION）
- 檔案結構文件
- 指令登記表
- 核心哲學
- 行為守則
- 衝突解決規則

這違反了深模組設計原則：一個模組的介面（讀取成本）應遠低於它提供的功能。CLAUDE.md 的介面（300 行全讀）幾乎等於它的內容本身。

**後果：**
- 任何協議變更都必須修改 CLAUDE.md
- Claude 每次 SESSION START 都必須讀完整份文件
- 很難測試「Claude 是否正確執行了 BEFORE CODING 的第 4 步」

**深化策略：** 提取生命週期協議為獨立可引用的 anchor，讓 CLAUDE.md 成為「只需讀一次的設定」，而非每次 session 重複讀取的記憶體。

---

### F2：knowledge/ 是無界成長的平坦巨型檔案（嚴重度：🔴 高）

**問題描述：**

`knowledge/patterns/index.md`、`knowledge/lessons-learned/index.md` 都是單一 Markdown 檔案，沒有分類、沒有標籤、沒有狀態欄位。

隨著條目增加：
- 讀取 1 個相關教訓 = 讀取整份 index.md（所有教訓都進入 context）
- 無法問「有沒有關於 Authentication 的教訓」，只能全讀後自己找
- 沒有條目的「狀態」（是否仍有效？是否已被更好的 pattern 取代？）

**深化策略：**
1. 加入 YAML frontmatter（`tags`、`status`、`phase`、`projects`）
2. 讓 `/query` 能做 tag-based 檢索而非全文掃描
3. 加入條目狀態（`✅ 驗證` / `🧪 實驗中` / `⚠️ 條件適用` / `❌ 已棄用`）

---

### F3：BEFORE CODING 是 N+1 讀取問題（嚴重度：🔴 高）

**問題描述：**

目前 BEFORE CODING 協議需要讀取：
```
functional.md（全部需求）
scope.md
existing-system.md
domain-knowledge.md
stakeholders.md
system-design.md
api-contracts.md
所有 ADR 檔案
patterns/index.md
tech-stack/index.md（可能）
_inferred.md
```

即使任務是「修復一個小 bug」，也可能讀進 10+ 個完整檔案。這是兩個問題疊加：
- **無差異讀取**：不管任務大小，讀取量相同
- **無前置摘要**：沒有方法快速判斷「這個檔案對這個任務相關嗎」

**深化策略：**

在 functional.md 和關鍵架構文件加入 `## 📌 Quick Context` 錨點，讓 Claude 先讀摘要，只在「摘要顯示相關」時才深讀全文。這個摘要由 `/save` 自動維護。

---

### F4：指令無前置條件宣告（嚴重度：🟡 中）

**問題描述：**

`/bug --uat` 假設 `bugs.md` 存在；`/close-project` 假設專案在 `wiki/index.md`；`/test-plan` 假設 `functional.md` 有確認需求。

但沒有任何一個指令宣告它的前置條件，結果是：
- 在未初始化的專案執行指令，會產生格式錯誤或靜默失敗
- Claude 只有在執行過程中才會遇到缺失的檔案，而不是在開始前就停止

**深化策略：** 每個指令加入 `## 前置條件` section（宣告式），Claude 在執行前主動驗證。違反前置條件時輸出清楚的錯誤，不繼續執行。

---

### F5：格式定義散落在指令檔案中（嚴重度：🟡 中）

**問題描述：**

REQ 格式定義在 `/ingest.md` 的 Phase 3-1 裡。PAT 格式在 `/self-improve.md` 裡。LESSON 格式在 `/self-improve.md` 和 `lessons-learned/index.md` 的兩個地方。

這導致：
- 沒有「唯一正確格式」的單一來源
- 修改格式時必須找到所有分散的定義並同步更新
- `/health-check` 無法讀取一個地方就知道「什麼是有效的 REQ」

**深化策略：** 建立 `knowledge/_schemas/` 目錄，集中存放所有格式 schema。所有指令引用 schema，不各自定義格式。

---

### F6：知識庫缺乏可測試性（嚴重度：🟡 中）

**問題描述：**

沒有辦法回答：
- 「functional.md 有沒有格式不完整的 REQ？」
- 「有沒有 _pending.md 的項目超過 60 天未解決？」
- 「所有 ADR 是否都有 決策 + 後果 兩個必填欄位？」
- 「知識庫的整體健康度是多少？」

目前唯一的驗證是透過 Claude 在作業過程中「碰到問題才發現」，屬於被動驗證。

**深化策略：** 建立 `/health-check` 指令，主動掃描並量化知識庫健康度。

---

### F7：_pending.md 和 _inferred.md 生命週期欄位貧乏（嚴重度：🟡 中）

**問題描述：**

_pending.md 的條目只有「等待回覆」一種狀態，缺乏：
- 緊急程度（是否阻塞目前 sprint？）
- 超過 X 天的自動升級機制
- 誰負責追蹤這條（多工程師時重要）

導致「重要的阻塞性問題」和「不急的邊緣澄清」混在一起，無法排序。

**深化策略：** 加入結構化的生命週期欄位：`**阻塞性**`（是/否）、`**優先級**`（🔴/🟡/🟢）、`**預期確認日**`。

---

### F8：知識條目間缺乏雙向連結（嚴重度：🟢 低）

**問題描述：**

教訓「LESSON-001：未確認需求就開始實作」與 BEFORE CODING 的守衛機制語意相關，但沒有顯式連結。PAT-AUTH-001 和相關的 LESSON 之間也沒有 link。

這讓「為什麼 BEFORE CODING 要做步驟 2？」這種問題無法快速從知識庫得到答案。

**深化策略：** 在 schema 中加入 `related_lessons`、`related_patterns` 選填欄位。

---

## 決策

分三個優先層實作深化改進：

### 層 1：立即實作（本次 session）

| 改動 | 解決的摩擦點 | 影響範圍 |
|------|-------------|----------|
| 建立 `knowledge/_schemas/` | F5 格式分散 | 所有指令 |
| 建立 `/health-check` 指令 | F6 無可測試性 | 維護流程 |
| knowledge 條目加 tags + status | F2 平坦巨型檔案 | `/query` 效率 |
| _pending / _inferred 加生命週期欄位 | F7 生命週期貧乏 | 待釐清管理 |
| 各指令加 `## 前置條件` | F4 無前置條件宣告 | 錯誤防護 |

### 層 2：下次 session 實作（需仔細處理）

| 改動 | 解決的摩擦點 | 需要注意 |
|------|-------------|----------|
| functional.md 加 Quick Context 錨點 | F3 N+1 讀取 | 要加到 /save 流程 |
| hot.md 加 YAML frontmatter | F1 God Module 部分 | 現有 hot.md 格式會變 |

### 層 3：評估後決定

| 改動 | 解決的摩擦點 | 風險 |
|------|-------------|------|
| 拆分 CLAUDE.md | F1 God Module | 高——涉及所有協議 |
| patterns/ 按子目錄分類 | F2 部分 | 中——需要遷移現有記錄 |

---

## 後果

**變得更容易的事：**
- 知道知識庫目前狀態（`/health-check`）
- 快速查詢「和 authentication 相關的教訓」（tags）
- 在指令執行前得到清楚的錯誤提示（前置條件）
- 新工程師接手時理解格式規範（schemas）

**需要定期維護的事：**
- 新增 pattern/lesson 時要填 tags 和 status
- _pending.md 新增條目時要判斷「是否阻塞性」

**不變的事：**
- 現有指令的觸發方式和使用流程
- use-cases.md 的覆蓋場景（維持 21 個）
- 需求三層分類（confirmed / pending / inferred）

---

## 行動項目

- [x] 建立 `knowledge/_schemas/req.md`、`pat.md`、`lesson.md`、`adr.md`
- [x] 建立 `.claude/commands/health-check.md`
- [x] 更新 `knowledge/patterns/index.md` 格式（加 tags、status）
- [x] 更新 `knowledge/lessons-learned/index.md` 格式（加 tags、phase、root_cause）
- [x] 更新 `projects/_example/01-requirements/_pending.md` 格式（加生命週期欄位）
- [x] 更新 `projects/_example/01-requirements/_inferred.md` 格式（加 impact 欄位）
- [x] `/ingest.md`、`/bug.md`、`/close-project.md` 加入前置條件
- [x] functional.md 加 Quick Context 錨點機制（實際做法：拆分為 `functional/{module}.md` 模組檔，各自含 Quick Context，見後續 session）
- [x] hot.md 格式加 YAML frontmatter + version（實際做法：拆分為 per-engineer `wiki/hot/{縮寫}.md`，含 engineer/updated frontmatter）
