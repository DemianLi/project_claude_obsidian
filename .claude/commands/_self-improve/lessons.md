# Phase 3：提取教訓 + 更新甲方偏好

## 3-A. 提取通用教訓（更新 knowledge/lessons-learned/）

識別本期踩過的坑（非第三方服務，或跨技術類型的）：
- 需求誤解
- 架構設計錯誤
- 溝通問題

```
識別到以下教訓：

[1] {教訓描述}（發生於 {專案}/{功能}）
    根因類型：需求誤解 / 架構錯誤 / 溝通問題 / 其他
    預防方式：{如何避免下次再犯}
    是否可以自動化？{例如：加入到 BEFORE CODING 的檢查清單}
    → 要新增至 lessons-learned/index.md？ (Y/n)
```

## 3-B. 更新甲方偏好（更新 03-client-context/stakeholders.md）

若累積了新的甲方偏好觀察：

```
識別到以下甲方偏好變化：

[1] {甲方名稱}
    新偏好：{偏好描述}
    觀察來源：{哪次 dev-note / session}
    → 要更新 stakeholders.md？ (Y/n)
```

範例：
- 「A 甲方喜歡在展示前先看 API 文件」
- 「B 甲方對術語 X 的定義和業界不同」

→ 完成後讀取 `_self-improve/health-report.md`
