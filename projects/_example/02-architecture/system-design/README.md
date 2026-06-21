# system-design/ — 系統架構元件目錄

此目錄存放各系統元件的詳細架構文件，是 `arch-index.md` 的深層內容層。

## 讀取規則

Claude **不直接讀取此目錄**，必須先讀 `../arch-index.md` 識別相關元件後才讀取對應檔案。

## 元件檔案命名

每個元件一個 `.md` 檔案，命名使用英文 slug：

```
system-design/
├── auth.md          # 認證與授權架構
├── order.md         # 訂單系統架構
├── payment.md       # 金流整合架構
├── notification.md  # 通知系統架構
├── database.md      # 資料庫設計與關係
├── infra.md         # 部署與基礎設施
└── ...
```

## 元件檔案結構（每個元件檔案的格式）

```markdown
---
type: system-design-component
component: {元件名}
project: {專案名}
updated: {YYYY-MM-DD}
---

# {元件中文名} 架構

## 📌 Quick Context
<!-- ⚡ Claude：確認本元件與當前任務相關後才讀此文件 -->
**職責**：{一句話說明此元件做什麼}
**邊界**：{明確說明此元件「不」做什麼}
**關鍵決策**：ADR-{ID}（{決策摘要}）
**最後變更**：{YYYY-MM-DD}（{變更摘要}）
<!-- /Quick Context -->

---

## 架構概覽

{說明此元件的設計動機、整體結構}

## 元件職責

{詳細說明做什麼、不做什麼}

## 資料流

{描述此元件的 input/output 和關鍵流程}

## 與其他元件的關係

| 元件 | 關係 | 說明 |
|------|------|------|
| {元件A} | 上游 / 下游 / 雙向 | {如何互動} |

## 關鍵設計決策

{記錄影響此元件的重要決策和取捨，詳細決策見 04-decisions/ADR-{ID}.md}

## 已知限制與風險

{此元件目前的技術債、已知問題、或未來可能需要重構的地方}
```

## 為何拆分元件

- 單一 system-design.md 累積至百頁時，Claude 讀整份文件是嚴重的 token 浪費
- 元件化後，一個認證元件檔案只有整體的 5–10%
- arch-index.md 的關鍵字路由確保 Claude 只讀相關元件
- 元件 Quick Context 讓 Claude 甚至可以在不讀完整元件的情況下判斷是否深讀
