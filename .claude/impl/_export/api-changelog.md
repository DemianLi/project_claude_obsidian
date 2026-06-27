# /export --api-doc 和 --changelog

---

## 模式一：API 文件（--api-doc）

讀取 `02-architecture/api-contracts.md`，生成標準 API 文件格式。

儲存至：`projects/{專案}/api-doc-v{版本}.md`

詢問：
```
① API 文件版本號？（例：v1.0.0）
② 是否包含請求/回應範例？（Y/n）
③ 目標讀者？（甲方技術團隊 / 第三方串接方 / 內部工程師）
```

文件格式：
```markdown
# {專案名稱} API 文件 v{版本}
更新日期：{YYYY-MM-DD}

## 端點索引
| 功能群組 | 方法 | 端點 | 說明 |
|----------|------|------|------|

## 端點詳細規格
### {功能群組}
#### {端點名稱}
- 方法：{GET/POST/PUT/DELETE}
- 路徑：{/api/xxx}
- 說明：{功能描述}
- 請求參數：{若有}
- 回應格式：{若有}
```

---

## 模式二：版本紀錄（--changelog）

從 `wiki/log.md` 和 `functional.md` 提取，
以使用者可選擇的版本範圍生成標準 CHANGELOG 格式。

詢問：
```
① 版本範圍？（例：從 v1.0.0 到 v1.2.0，或「全部」）
② 目標讀者？（甲方 / 內部）
```

更新至：`projects/{專案}/CHANGELOG.md`（append 新版本，不覆蓋舊記錄）

格式：
```markdown
## [v{版本}] — {YYYY-MM-DD}

### 新增功能
- {功能名稱}：{一句話描述}（REQ-FXXX）

### 修改功能
- {功能名稱}：{變更說明}（CR-XXX）

### 修復問題
- {問題描述}（BUG-XXX）

### 已知問題
- {若有}
```

完成後 append 記錄至 `wiki/log.md`。
