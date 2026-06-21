# /export — 交付文件生成

## 觸發方式
```
/export                    （互動式詢問用途後路由）
/export --client           （甲方系統交付文件）
/export --handover         （工程師技術交接文件）
/export --onboarding       （新工程師導覽文件）
/export --api-doc          （API 文件）
/export --changelog        （版本紀錄）
```

## 前置條件
```
[ ] projects/{專案}/00-overview.md 存在
[ ] 若 --client：functional.md 至少有 ✅ 需求
[ ] 若 --handover / --onboarding：全專案知識庫已建立
```

## 執行路由（每次只讀當前模式的子文件）

| 旗標 | 讀取 | 輸出路徑 |
|------|------|----------|
| `--client` | `_export/client.md` | `06-qa-testing/delivery-doc-v{版本}.md` |
| `--handover` | `_export/handover.md` | `handover-doc-{YYYY-MM-DD}.md` |
| `--onboarding` | `_export/onboarding.md` | `onboarding-{YYYY-MM-DD}.md` |
| `--api-doc` | `_export/api-changelog.md` → api-doc 節 | `api-doc-v{版本}.md` |
| `--changelog` | `_export/api-changelog.md` → changelog 節 | `CHANGELOG.md` |
| 無旗標 | 詢問用途後路由至對應模式 | — |

## 原則
- 輸出為獨立文件，**不修改**知識庫原始檔案
- 完成後 append 記錄至 `wiki/log.md`
