---
tags: [database, abstraction, testability, architecture, orm]
status: experimental
projects: []
---

# PAT-DB-001：Repository Pattern

**驗證次數**：0 次（預設模式）
**適用情境**：需要抽象 DB 操作、方便測試的後端服務；預期未來可能換 ORM 或 DB
**不適用情境**：小型快速開發（CRUD 簡單的 prototype），overhead 大於收益
**參考工時**：初次搭建 Repository 層約 4-8 小時；後續每個 entity 約 1-2 小時

## 實作要點

```
Service → Repository Interface → Repository Implementation → DB
```

## 注意事項

- 小專案 overhead 高，在決定使用前評估是否有測試需求
- Repository Interface 要夠薄，不要把 SQL 語法泄漏到 interface 層

## 相關資源

- **相關教訓**：（待填入）
