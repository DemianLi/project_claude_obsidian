# /export --handover — 工程師技術交接文件

## 讀取來源
```
全部 projects/{專案}/ 內容
knowledge/patterns/ 和 knowledge/lessons-learned/（與本案相關的）
```

## 生成文件

儲存至：`projects/{專案}/handover-doc-{YYYY-MM-DD}.md`

```markdown
# {專案名稱} 技術交接文件
交接日期：{YYYY-MM-DD}｜交接人：{使用者}｜接手人：{若已知}

## 必讀文件（依順序）
1. 00-overview.md — 專案背景與甲方資訊
2. 01-requirements/functional.md — 所有確認需求
3. 01-requirements/scope.md — 合約範疇邊界
4. 02-architecture/system-design.md — 系統架構
5. 03-client-context/existing-system.md — 甲方技術環境限制
6. 03-client-context/domain-knowledge.md — 領域術語
7. 04-decisions/ — 所有技術決策（ADR）
8. 01-requirements/_pending.md — 待甲方確認的問題
9. 01-requirements/_inferred.md — 未驗證的推測與缺口

## 現有系統概況
### 技術棧：{從 system-design 提取}
### 資料庫結構要點：{核心 table 和重要關聯}
### 已知技術限制：{從 existing-system 提取}

## 重要技術決策（ADR 摘要）
{每個 ADR 一句話摘要，附連結}

## 未解決問題清單
### 待甲方確認（_pending.md）：{列出所有未解決 PENDING}
### 待驗證的推測（_inferred.md）：{列出高風險 INF/GAP}

## 已知地雷
{從 lessons-learned 找與本案技術棧相關的教訓}

## 甲方關係人
{從 stakeholders.md 提取，含聯絡方式和偏好}

## 目前未完成事項
需求進度：{狀態非完成的 REQ}
未關閉 Bug：{BUG-ID + 描述}
```
