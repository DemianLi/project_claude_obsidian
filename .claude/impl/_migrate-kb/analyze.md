# Phase 1：分析現有文件，建議模組分組

## 1-A. 需求模組分析（--target=reqs）

讀取 `functional.md` 全文，分析：
1. 總需求數量
2. 各需求的業務域關鍵字（從標題與描述推斷）
3. 建議的模組分組（每個模組 10-50 條需求）

```
📊 遷移分析｜{專案名稱}

現有需求：{N} 條
建議模組分組：

模組名           需求數   代表需求（樣本）
──────────────   ──────   ──────────────────
auth             {N} 條   REQ-F001 REQ-F002...
order            {N} 條   REQ-F010 REQ-F012...
payment          {N} 條   REQ-F020...

確認此分組方案？（Y / 調整模組名稱 / 調整歸屬）
```

## 1-B. 架構元件分析（--target=arch）

讀取 `system-design.md` 全文，識別各架構段落：
```
識別到以下架構段落：
- §{段落名} → 建議 system-design/{slug}.md
確認？(Y / 調整)
```

## 1-C. API 群組分析（--target=api）

讀取 `api-contracts.md` 全文，識別端點群組（每群組 10-30 個端點）：
```
識別到以下 API 群組：
- {群組名} ({N} 個端點) → api-contracts/{module}.md
確認？(Y / 調整)
```

**若使用者調整 → 重新呈現分組方案後再確認。**

若 `--dry-run`：在此停止，不繼續讀取後續 Phase。
否則 → 確認後讀取對應的 `_migrate-kb/reqs.md` 或 `_migrate-kb/arch-api.md`
