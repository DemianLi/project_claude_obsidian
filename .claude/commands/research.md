# /research — 知識庫驅動的網路搜索與解方驗證

## 觸發方式
```
/research [主題]              （針對特定技術問題搜索最佳解方）
/research [主題] --deep       （多輪搜索，交叉驗證多個來源）
```

## 設計原則

一般網路搜索給通用答案，不考慮「這個專案的 MySQL 不能升版」「甲方 Server 是 Windows 不能跑 Docker」。
本指令先從知識庫讀出「約束輪廓」，帶著約束去搜，找到後再回頭驗證相容性：

```
知識庫約束 + 問題描述 → 精準搜索 → 相容性驗證 → 排名結果
```

## 前置條件
```
[ ] projects/{專案}/03-client-context/existing-system.md 存在（建議）
```

## 執行序列（每次只讀當前 Phase 的子文件）

| Phase | 讀取 | 說明 |
|-------|------|------|
| 1 | `_research/constraints.md` | 從知識庫讀取約束輪廓 |
| 2 | `_research/query.md` | 構建精準搜索查詢 |
| 3 | `_research/search.md` | 執行網路搜索（3-5 個候選方案） |
| 4 | `_research/verify.md` | 相容性驗證 + 理解確認 |
| 5 | `_research/output.md` | 呈現排名結果 + 後續行動（ADR / 更新 log） |

## --deep 模式

在 Phase 3 完成後，額外執行：
- Round 2：交叉驗證（搜索「{方案 A} problems / pitfalls」）
- Round 3：替代方案掃描（「alternatives to {方案 A}」）
- Round 4：版本相容性確認
