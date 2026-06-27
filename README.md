# 軟體工程知識庫 — Claude 協作系統

軟體服務工程師的 AI 協作知識庫。將甲方文件、系統分析、開發決策整理為結構化知識，
讓 Claude 在每次開發前自動查閱背景，減少實作錯誤率並透過自我優化持續提升協作品質。

---

## 必要工具

| 工具 | 用途 | 安裝方式 |
|------|------|----------|
| **Claude Code** | 執行 slash commands，讀取知識庫 | 見下方步驟 |
| **Obsidian**（建議） | 視覺化查看知識庫、圖形化連結 | [obsidian.md](https://obsidian.md) 免費下載 |
| **Git**（建議） | 版本控制知識庫，追蹤每次變更 | [git-scm.com](https://git-scm.com) |

---

## 安裝步驟

### Step 1：安裝 Claude Code

Claude Code 是 Anthropic 提供的命令列工具，讓 Claude 可以讀取你的專案資料夾並執行指令。

**macOS / Linux：**
```bash
npm install -g @anthropic-ai/claude-code
```

**Windows：**
```bash
npm install -g @anthropic-ai/claude-code
```

> 需要先安裝 [Node.js 18+](https://nodejs.org)

驗證安裝：
```bash
claude --version
```

### Step 2：取得此知識庫

**方法 A：從 GitHub clone（推薦）**
```bash
git clone https://github.com/{你的帳號}/{repo名稱}.git
cd {repo名稱}
```

**方法 B：直接複製資料夾**
將整個資料夾複製到你想要的位置即可，無需 git。

### Step 3：在 Claude Code 開啟

```bash
cd /path/to/claude_obsidien_setting
claude
```

Claude Code 會自動讀取 `CLAUDE.md`，載入所有協作指引與指令。

你會看到 Claude 回應：
```
✅ 知識庫已載入
目前狀態：系統就緒，尚無進行中專案
建議下一步：執行 /project-init 建立你的第一個專案
```

### Step 4：（建議）在 Obsidian 開啟

1. 下載並安裝 [Obsidian](https://obsidian.md)
2. 開啟 Obsidian → **管理保險庫 → 以資料夾開啟保險庫**
3. 選擇此資料夾

Obsidian 可以視覺化呈現需求、決策、架構之間的連結關係，建議搭配使用。

### Step 5：（選用）啟用 Obsidian MCP 讓 Claude 直接讀寫

若希望 Claude 能直接讀寫 Obsidian 的筆記，安裝 Local REST API 插件：

1. Obsidian → 設定 → 社群插件 → 搜尋「Local REST API」→ 安裝並啟用
2. 複製 API Key
3. 執行：
```bash
claude mcp add-json obsidian-vault '{
  "type": "stdio",
  "command": "uvx",
  "args": ["mcp-obsidian"],
  "env": {
    "OBSIDIAN_API_KEY": "貼上你的API Key",
    "OBSIDIAN_HOST": "127.0.0.1",
    "OBSIDIAN_PORT": "27124"
  }
}' --scope user
```

> 沒有 MCP 也可以正常使用，Claude Code 會直接讀寫資料夾內的 markdown 檔案。

---

## 團隊共用設定（多工程師 + 獨立 CODE_ROOT）

> 適用情境：團隊有多位工程師，各自在自己機器上開發同一批程式碼專案（CODE_ROOT，例如 `~/Projects_dotnet/{project_name}`），希望開發時也能用上知識庫的 `CLAUDE.md` 行為邏輯與 17 個 slash commands，但不想把知識庫的 `.claude/` 複製進程式碼專案（複製會導致更新不同步）。

> ⚠️ **前提（兩層都依賴這個，不是只有指令層）**：每位工程師的 KB clone 必須在同一個慣例路徑 `~/Projects_vibecoding/claude_obsidien_setting`。`{CODE_ROOT}/CLAUDE.md` 裡寫死的 `KB_ROOT: ~/Projects_vibecoding/claude_obsidien_setting` 是 git 共用、對所有人一字不差的同一份檔案——若某人的 KB clone 在別的路徑，這份指引會指向一個不存在的路徑，行為層**會靜默失效**（Claude 讀不到 KB 的 CLAUDE.md，但不會明顯報錯，只是 BEFORE CODING 等邏輯沒有套用）。下方指令層的 symlink 也是用同一個路徑。若團隊習慣的路徑不同，兩處（這份 KB clone 路徑 + `{CODE_ROOT}/CLAUDE.md` 裡的 `KB_ROOT`）要一起改。

兩層**必須一起設好**才能讓 `/bug`、`/query` 等指令真正運作：指令層只負責讓 `/bug` 這個語法被 Claude Code 認得（觸發去讀 dispatcher 檔案）；dispatcher 檔案內部引用的 `{KB_ROOT}/.claude/impl/...` 路徑，要靠行為層先把 `KB_ROOT` 的定義載入 context 才能正確解析。只設指令層、沒設行為層，指令會「打得動但讀不到內容」。

**行為層（BEFORE CODING 等邏輯，定義 `KB_ROOT`）—— 通常不需要額外設定**

只要這個專案是用 `/project-init` 建立的，`{CODE_ROOT}/CLAUDE.md` 就已經包含「先讀 `{KB_ROOT}/CLAUDE.md`」的指引。這份檔案是程式碼 repo 的一部分，工程師 clone/pull 程式碼倉庫時自動拿到，**不需要每人手動設定**——但仍受上方路徑前提約束。

若專案不是這樣建立的（例如先有程式碼才導入知識庫），手動在 `{CODE_ROOT}/CLAUDE.md` 補上一段，內容比照 `/project-init` Step 6 產生的範本（見 `.claude/commands/project-init.md`）。

**指令層（`/bug`、`/query` 等 17 個指令）—— 每人本機一次性設定**

Slash commands 只會在「目前專案自己的 `.claude/commands/`」或「全域 `~/.claude/commands/`」被掃描到，沒有跟著 git 自動同步的機制。每位工程師在自己機器上執行一次：

```bash
# 先確認沒有已存在的個人全域指令會被蓋掉
ls ~/.claude/commands 2>/dev/null && echo "⚠️ 已存在內容，改用下方逐檔 symlink，勿覆蓋整個資料夾"

# 確認沒有衝突後，整資料夾 symlink：
ln -s ~/Projects_vibecoding/claude_obsidien_setting/.claude/commands ~/.claude/commands
```

若 `~/.claude/commands` 已有個人指令，改成逐檔 symlink：
```bash
for f in ~/Projects_vibecoding/claude_obsidien_setting/.claude/commands/*.md; do
  ln -s "$f" ~/.claude/commands/
done
```

設好之後：
- 在任何目錄（包含 `~/Projects_dotnet/{project_name}`）都能直接打 `/bug`、`/query`、`/save` 等全部 17 個指令，且能正確解析到 KB 內容（前提是行為層也已生效，見上方）
- KB 的 commands 或 `.claude/impl/` 之後任何更新，因為是 symlink + 絕對路徑讀取，**即時生效**，不需要重新設定

**跨平台差異**

上方指令在 macOS / Linux 已實測通過（`claude -p` 在完全隔離的測試目錄下驗證過指令層與行為層都正確運作）。Windows 工程師依環境不同：

| 環境 | 做法 | 備注 |
|------|------|------|
| Windows 原生（PowerShell/CMD，不透過 WSL） | 用 **junction** 取代 symlink：`mklink /J "%USERPROFILE%\.claude\commands" "%USERPROFILE%\Projects_vibecoding\claude_obsidien_setting\.claude\commands"` | Junction 是目錄層級連結，不需要系統管理員權限或 Developer Mode（一般 symlink `mklink /D` 才需要）。⚠️ 未實機測試過，建議第一位 Windows 工程師先驗證一次再讓其他人照做 |
| WSL（Windows 上用 Linux 子系統跑 Claude Code） | 跟 macOS/Linux 相同，用 `ln -s` | ⚠️ 知識庫 clone 必須跟 Claude Code 執行環境在**同一個檔案系統**內（同樣在 WSL 裡，不要混用 Windows 原生路徑），否則 symlink 會直接失效 |

---

## 第一次使用

### 1. 建立你的第一個專案

在 Claude Code 中輸入：
```
/project-init
```

Claude 會詢問專案名稱和基本資訊，然後建立完整的資料夾結構。

### 2. 匯入甲方文件

將甲方提供的文件（PDF、Word、email 文字）放入 `_inbox/` 資料夾，然後：
```
/ingest
```

或直接把文字貼給 Claude：
```
/ingest [貼上甲方文件內容]
```

### 3. 開始開發

直接告訴 Claude 你要做什麼，例如：
```
幫我實作用戶登入功能
```

Claude 會自動查閱知識庫，確認需求狀態後再開始實作。

### 4. 結束 Session

```
/save
```

---

## 指令速查

| 分類 | 指令 | 說明 |
|------|------|------|
| 需求管理 | `/project-init` | 建立新專案資料夾結構 |
| | `/ingest` | 解析甲方文件，三階段確認後寫入知識庫 |
| | `/reverse-engineer` | 逆向分析舊系統程式碼/DB，區分事實、推測、邏輯缺口 |
| | `/query [問題]` / `--verify` | 查詢知識庫記錄 / 驗證 Claude 對術語需求的理解是否正確 |
| | `/reconcile` | 清理已解決的待釐清項目，合併重複條目 |
| | `/health-check` | 檢查知識庫結構完整性與索引一致性 |
| 範疇變更 | `/cr` | 登記變更請求（超出合約範疇的新需求） |
| | `/impact` | 分析需求/架構變更的影響範疇與工時 |
| 開發輔助 | `/research [主題]` | 帶著專案約束條件搜索網路，驗證解方相容性 |
| | `/test-plan` | 從已確認需求自動產生測試計畫 |
| | `/bug` | 記錄 bug 或批次處理 UAT 回饋 |
| 報告交付 | `/report` | 產生甲方可讀的進度報告 |
| | `/export` | 匯出交付文件（甲方版/技術交接版/新人導覽版） |
| 收尾 | `/close-project` | 專案收尾：快照、CHANGELOG、封存 |
| Session | `/save` | 儲存 session，更新熱快取 |
| | `/self-improve` | 從開發筆記提煉模式與教訓，優化知識庫 |
| | `/migrate-kb` | 將舊格式（扁平檔）專案遷移為分檔索引格式 |

---

## 知識庫結構

知識庫（KB_ROOT）和程式碼是分開的兩個 repo：知識庫放需求/架構/決策，程式碼放在各專案自己的資料夾（路徑不限，例如 `~/Projects_dotnet/{project_name}`），執行 `/project-init` 時會問你程式碼路徑並自動產生薄版 `CLAUDE.md` 連接兩者；多工程師各自在自己機器開發同一批程式碼的設定見下方「團隊共用設定」。

```
claude_obsidien_setting/          ← KB_ROOT
├── CLAUDE.md                    # Claude 自動讀取的協作指引（核心）
├── README.md                    # 本文件
├── _inbox/                      # 甲方文件丟放區
│   └── _unassigned/             # 尚未確認歸屬的文件暫存
├── _templates/                  # Obsidian 筆記模板
├── wiki/
│   ├── hot/{工程師縮寫}.md      # 各工程師最近工作脈絡（/save 自動更新）
│   ├── index.md                 # 所有專案目錄與狀態
│   └── log.md                   # Append-only 操作日誌
├── projects/
│   └── {專案名}/
│       ├── 00-overview.md       # 專案總覽
│       ├── 01-requirements/
│       │   ├── functional-index.md  # ⚡ 需求薄索引 → functional/{module}.md（各模組詳細需求，✅ 才可實作）
│       │   ├── scope.md             # 合約範疇邊界
│       │   ├── _pending/_index.md   # ⚡ 🕐 待甲方澄清（各條一檔）
│       │   └── _inferred/_index.md  # ⚡ 🔍 推測 + ❓ 邏輯缺口（各條一檔，禁止作為實作依據）
│       ├── 02-architecture/
│       │   ├── arch-index.md        # ⚡ 元件地圖 → system-design/{component}.md
│       │   ├── api-contracts/index.md  # ⚡ → api-contracts/{group}.md
│       │   └── _legacy-analysis.md  # 逆向工程結構性事實（選配）
│       ├── 03-client-context/
│       │   ├── stakeholders.md
│       │   ├── existing-system.md
│       │   └── domain-knowledge.md  # 產業術語、業務流程
│       ├── 04-decisions/        # Architecture Decision Records
│       ├── 05-dev-notes/        # 每次 session 的開發筆記
│       ├── 06-qa-testing/
│       │   ├── bugs-active.md   # ⚡ 未關閉 bug 薄索引 → bugs/{BUG-ID}.md
│       │   └── bugs/
│       └── CHANGELOG.md
└── knowledge/
    ├── patterns/index.md        # 跨專案可複用的設計模式
    ├── tech-stack/index.md      # 技術棧心得與踩坑記錄
    └── lessons-learned/index.md # 教訓清單
```

> ⚡ 標記的是「薄索引」——Claude 永遠先讀這些，再依交集深讀對應的個別檔案，避免整份知識庫被讀進 context。

---

## 設計原則

**風險分配：** Claude 整理資訊、識別問題、提供選項；你做所有業務決策。
有任何不確定，Claude 給選項等你決定，不靜默自行判斷。

**三層需求隔離：**
```
functional/{module}.md（✅ 確認）→ 可實作
_pending/{ID}.md（🕐 待確認）→ 禁止實作
_inferred/{ID}.md（🔍 推測）→ 禁止實作，必須驗證後升格
```

**知識複利：** 每個 session 的 dev-notes 透過 `/self-improve` 提煉為跨專案的 patterns 和 lessons，下個專案直接複用。

---

## 常見問題

**Q：不用 Obsidian 可以嗎？**
可以。所有檔案都是純 markdown，用任何編輯器都能查看。Obsidian 只是讓你能看到連結關係的圖形視覺化。

**Q：Claude Code 和一般 Claude（網頁版）有什麼差別？**
Claude Code 可以直接讀寫你電腦上的檔案，並執行 slash commands（`/ingest`、`/save` 等）。網頁版的 Claude 無法直接操作本地檔案。

**Q：知識庫可以多人共用嗎？**
可以，且是設計上就支援的。每位工程師有自己的 `wiki/hot/{縮寫}.md`，`/save` 只替換自己的檔案；bug、待釐清項目、推測/缺口都是一條一檔（`bugs/{ID}.md`、`_pending/{ID}.md`、`_inferred/{ID}.md`），多人同時新增不會互相衝突。專案內 `collab/{縮寫}.md` 記錄各自鎖定的項目，BEFORE CODING 會自動偵測鎖定衝突——不只 `functional/{module}.md` 的 REQ，`02-architecture/` 下的元件設計與 API 群組也適用同一套鎖定機制（細節見 `wiki/collab-protocol.md`）。`scope.md`、`wiki/index.md`、`03-client-context/*.md` 這類無法拆成獨立記錄的整份共用文件，靠「異動前提示確認最新版本、異動後留 log」降低衝突，不是鎖定。多工程師各自在獨立 CODE_ROOT 開發的設定見上方「團隊共用設定」。

**Q：如何備份？**
知識庫（KB_ROOT）的版控由 **Obsidian git 插件自動管理**，不需要手動 commit/push。程式碼倉庫（CODE_ROOT）則由工程師自行 git 管理。

---

*基於 [claude-obsidian](https://github.com/AgriciDaniel/claude-obsidian) 概念，為軟體服務工程師場景定制。*
