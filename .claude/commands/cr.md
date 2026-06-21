# /cr — 變更請求（Change Request）正式流程

## 觸發方式
```
/cr [需求描述]       （登記新的變更請求）
/cr --list           （列出所有 CR 狀態）
/cr --approve CR-{N} （核准 CR，更新知識庫）
/cr --reject CR-{N}  （拒絕 CR，記錄原因）
```

## ⚠️ 使用時機（必須先 /cr，不得直接 /ingest）
- 甲方需求不在 `scope.md` 的原始合約範圍內
- 已確認需求發生實質性變更（非描述釐清，而是功能本身改變）
- 需求追加導致工時或費用可能增加

## 前置條件
```
[ ] projects/{專案}/01-requirements/scope.md 存在
[ ] 若 --approve/--reject：04-decisions/CR-{N}-*.md 存在
```

## 執行路由（每次只讀當前模式的子文件）

| 觸發 | 讀取 | 說明 |
|------|------|------|
| `/cr [描述]` | `_cr/new.md` | 登記 CR + 建立草稿 |
| `--approve` | `_cr/approve.md` | 核准：更新 scope + /ingest + 更新 CR 狀態 |
| `--reject` | `_cr/reject-list.md` → reject 節 | 拒絕：更新 scope + 記錄原因 |
| `--list` | `_cr/reject-list.md` → list 節 | 列出所有 CR 清單 |

## 與其他指令的關係
```
甲方提出新需求
  ├─ 在原始合約範圍內？是 → /ingest
  └─ 否/不確定 → /cr [此指令]
       ├─ /impact 分析影響範疇（建議核准前執行）
       └─ /cr --approve 或 /cr --reject
```
