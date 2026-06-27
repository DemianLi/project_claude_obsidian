# /export --onboarding — 新工程師導覽文件

## 詢問接手情境
```
① 接手原因？(A) 原工程師離職  (B) 增員  (C) 臨時支援  (D) 其他
② 緊急程度？(A) 立即接（本週上線）  (B) 正常交接（2 週）  (C) 提前佈局（1 個月+）
③ 接手者技術背景？（與本案技術棧相似 / 熟悉度未知）
```

## 生成文件

儲存至：`projects/{專案}/onboarding-{YYYY-MM-DD}.md`

文件結構：

```
## 🚨 30 分鐘緊急摘要（立即接手必讀）
- 系統在做什麼（一句話）
- 目前開發階段
- 最近 3 次 log.md 記錄
- 最需要注意的地雷（前 3 條）
- 緊急聯絡人

## 📚 正式上手路線圖

### P0：第 1 天理解（約 2 小時）
[P0-1] 00-overview.md — 專案全貌（30 分鐘）
[P0-2] scope.md + _pending/_index.md — 邊界與風險（30 分鐘）
[P0-3] existing-system.md — 甲方環境限制（30 分鐘）
[P0-4] 04-decisions/ 全部 ADR — 已定案的技術決策（30 分鐘）

### P1：第 1 週掌握（約 6 小時）
[P1-1] functional-index.md + 各 functional/{module}.md — 完整功能需求（1 小時）
[P1-2] arch-index.md + system-design/ + api-contracts/ — 系統架構（2 小時）
[P1-3] domain-knowledge.md — 甲方業務語言（1 小時）
[P1-4] _inferred/_index.md — 未解決技術問題（1 小時）
[P1-5] bugs-active.md — 目前 Bug 狀態（30 分鐘）

### P2：第 1 個月按需查閱
05-dev-notes/ / knowledge/patterns/ / lessons-learned/ / tech-stack/

## 🤔 常見問題（Claude 根據知識庫預先回答）
Q1: 系統在哪個開發階段，還有什麼沒做？
Q2: 有什麼不能動的地方？
Q3: 最容易踩雷的地方？
Q4: 甲方技術環境有什麼特殊限制？
Q5: 為什麼這樣設計 {核心功能}？

## 📞 快速問答（可直接問 Claude）
「REQ-F{N} 這條需求是什麼意思？」
「{功能} 的架構決策是什麼？」
「{術語} 在這個系統裡是什麼意思？」

## ✅ 第一週 Checklist
- [ ] 讀完所有 P0 文件（4 個，約 2 小時）
- [ ] 能用一句話解釋系統在做什麼
- [ ] 知道未完成需求和未關閉 Bug
- [ ] 知道甲方環境最重要限制
- [ ] 執行 /query --verify [最重要業務術語] 確認理解正確
```
