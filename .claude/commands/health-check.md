---
description: 檢查知識庫結構完整性與索引一致性
---
# /health-check — 知識庫健康度診斷

## 觸發方式
```
/health-check                  （掃描所有進行中專案）
/health-check {專案名稱}       （只掃描指定專案）
/health-check --schemas        （只驗證格式合規性）
/health-check --stale          （只報告過期與孤立項目）
```

## 前置條件
```
[ ] wiki/index.md 存在（用於識別進行中專案）
[ ] 指定專案：projects/{專案名}/ 存在
```

## 執行路由（每次只讀當前模式的子文件）

| 旗標 | 讀取序列 | 說明 |
|------|----------|------|
| 無旗標 | `structure.md` → `schema.md` → `stale.md` → `knowledge.md` → `report.md` | 完整診斷（5 個 Phase） |
| `--schemas` | 只讀 `_health-check/schema.md` | 只驗證格式合規性 |
| `--stale` | 只讀 `_health-check/stale.md` | 只報告過期與孤立項目 |

## 子文件對應

| 文件 | 內容 |
|------|------|
| `_health-check/structure.md` | Phase 1：必要檔案存在性檢查 |
| `_health-check/schema.md` | Phase 2：REQ / ADR / PAT / LESSON 格式驗證 |
| `_health-check/stale.md` | Phase 3：_pending 年齡、INF 風險、ADR 孤立、Bug 老化 |
| `_health-check/knowledge.md` | Phase 4：跨專案 knowledge/ 健康度 |
| `_health-check/report.md` | Phase 5：健康度報告 + 快速修復建議 |

建議執行時機：每次 `/self-improve` 前 / 新工程師加入前 / `/close-project` 前
