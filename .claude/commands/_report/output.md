# Phase 4：輸出

## --format email（預設）

呈現報告內容後，提示：
```
✅ 報告已生成

以上內容可直接複製後貼入 email。
要我存成 markdown 檔案嗎？（/report --format markdown）
```

## --format markdown

儲存至：`projects/{專案}/05-dev-notes/report-{起}~{迄}.md`

## 完成後

append 一筆記錄至 `wiki/log.md`：
```
### [{日期}] {專案} — 生成進度報告（{起} ~ {迄}）
- 對象：{甲方 / 內部}
- 完成需求：{N} 條 / 進行中：{N} 條 / blockers：{N} 條
```
