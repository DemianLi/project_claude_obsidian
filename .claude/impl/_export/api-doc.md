# /export --api-doc — API 文件

讀取 `02-architecture/api-contracts/index.md`，再讀各群組 `api-contracts/{module}.md`，生成標準 API 文件格式。

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
