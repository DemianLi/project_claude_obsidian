# Phase 1：建立約束輪廓（從知識庫讀取）

從以下檔案提取與問題相關的限制條件：

**技術約束**（`03-client-context/existing-system.md`）
```
OS / 部署環境：{例：Windows Server 2016，無 Docker}
程式語言 / 框架：{例：PHP 7.4 / Laravel}
資料庫：{例：MySQL 5.7，不可升版}
外部系統整合：{例：必須串接現有 AD 帳號系統}
網路限制：{例：無法對外連網}
```

**領域約束**（`03-client-context/domain-knowledge.md`）
```
關鍵術語：{提取與問題相關的術語定義}
業務規則：{影響技術選型的業務限制}
法規要求：{例：個資法、HIPAA 等}
```

**品質約束**（`01-requirements/non-functional.md`，若存在）
```
效能指標：{例：API < 500ms P95}
安全要求：{例：必須支援 RBAC}
相容性要求：{例：需支援 IE11}
```

**已有的技術決策**（`04-decisions/`）
```
既有 ADR：{列出相關的技術決策，避免搜出與已決定方向衝突的方案}
```

→ 整合為「約束輪廓摘要」，完成後讀取 `_research/query.md`
