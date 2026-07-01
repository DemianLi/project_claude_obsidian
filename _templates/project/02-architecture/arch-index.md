---
type: arch-index
project: {project_name}
updated: {YYYY-MM-DD}
---

# 架構元件索引

<!-- ⚡ Claude 讀取規則：
  1. 讀此索引 → 比對下方「系統元件地圖」任務關鍵字 → 識別相關元件
  2. 只讀 system-design/{對應元件}.md，不讀其他元件檔案
  3. api-contracts/index.md 只在需要確認 API 規格時才讀（任務包含「API 呼叫/端點」時），再由其路由至相關群組檔案
  4. _legacy-analysis.md 只在逆向工程 / 整合案才讀
-->

---

## 系統元件地圖

<!-- ⚡ Claude：讀此表 → 比對任務關鍵字 → 只讀對應的元件檔案 -->

| 元件 | 說明 | 詳細檔案 | 任務關鍵字 |
|------|------|---------|-----------|
| （目前無） | — | — | — |

<!-- 新增元件時在此表格追加一行，同時建立對應的 system-design/{slug}.md 檔案 -->

---

## 架構文件清單

```
02-architecture/
├── arch-index.md                 ← 你在這裡（永遠先讀）
├── system-design/
│   ├── README.md                 ← 說明元件分檔結構
│   └── {slug}.md                 ← 各元件架構（建立元件時新增）
├── api-contracts/
│   ├── index.md                  ← API 薄索引（先讀）
│   ├── README.md                 ← 說明群組結構
│   └── {slug}.md                 ← 各群組端點規格（建立群組時新增）
└── _legacy-analysis.md           ← 逆向工程結果（整合案才需要）
```

---

## 讀取決策樹（Claude 使用）

<!-- 每建立一個元件，依其任務關鍵字在下方補上一條判斷分支 -->

```
任務描述 → 判斷

（目前無元件，尚無判斷分支。建立第一個元件後依「元件：任務關鍵字」的對應關係補上，例：
  包含「登入/Token/權限」→ 讀 system-design/{對應元件}.md）

若任務涉及 API 呼叫/端點
  → 讀 api-contracts/index.md，由其路由至相關群組檔案

若任務跨多個元件 → 分別讀取各相關元件檔案

若 system-design/ 目錄不存在（舊格式）：
  → fallback 讀 system-design.md 全文
  → 提示：「建議執行 /migrate-kb 拆分為元件格式」
```
