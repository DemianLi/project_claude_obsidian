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
cd /path/to/{你的知識庫資料夾}
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

- **KB_ROOT**：知識庫路徑，即 CLAUDE.md 所在目錄——全團隊只要統一 clone 在同一個位置即可，路徑本身不需要寫死在任何設定裡（下方範例用 `~/{你的知識庫資料夾}` 代稱實際路徑）
- **CODE_ROOT**：程式碼實際所在目錄（例：`~/Projects_dotnet/{project_name}`），由 `/project-init` 產生的薄 CLAUDE.md 隨 git 自動同步給全員

每位工程師在自己機器上執行一次，讓 `/bug`、`/query` 等 17 個指令在任何目錄都能用：

**macOS / Linux**
```bash
ln -s ~/{你的知識庫資料夾}/.claude/commands ~/.claude/commands
```

**Windows（PowerShell/CMD）**
```cmd
mklink /J "%USERPROFILE%\.claude\commands" "%USERPROFILE%\{你的知識庫資料夾}\.claude\commands"
```

**WSL**：跟 macOS/Linux 相同，用 `ln -s`。

---

## 指令速查

| 分類 | 指令 |
|------|------|
| 需求管理 | `/project-init` `/ingest` `/reverse-engineer` `/query` `/reconcile` `/health-check` |
| 範疇變更 | `/cr` `/impact` |
| 開發輔助 | `/research` `/test-plan` `/bug` |
| 報告交付 | `/report` `/export` |
| 收尾 | `/close-project` |
| Session | `/save` `/self-improve` `/migrate-kb` |

每個指令的完整說明見對應的 `.claude/commands/{指令}.md`；常見場景的完整操作流程見 [`wiki/playbook.md`](wiki/playbook.md)。

---

## 知識庫結構

知識庫（KB_ROOT）和程式碼是分開的兩個 repo：知識庫放需求/架構/決策，程式碼放在各專案自己的資料夾（路徑不限，例如 `~/Projects_dotnet/{project_name}`），執行 `/project-init` 時會問你程式碼路徑並自動產生薄版 `CLAUDE.md` 連接兩者；多工程師各自在自己機器開發同一批程式碼的設定見上方「團隊共用設定」。

```
{你的知識庫資料夾}/                ← KB_ROOT
├── projects/{專案名}/            # 各甲方專案：需求 / 架構 / 決策 / 測試
├── knowledge/                    # 跨專案沉澱：patterns / lessons-learned / tech-stack
└── wiki/                         # 個人知識層：hot/{縮寫}.md / index.md / log.md / concepts / entities / sources / questions
```

完整目錄結構（每份檔案的用途、⚡ 薄索引標記）見 [`.claude/protocols/structure-map.md`](.claude/protocols/structure-map.md)，不在這裡重複維護一份。

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
