# /project-init — 建立新專案

## 觸發方式
```
/project-init [專案名稱]
```

## 執行步驟

收到此指令後，依序執行：

**1. 確認專案名稱**
若未提供名稱，詢問：「專案名稱是什麼？（建議用英文或拼音，例如：eshop-acme 或 erp-client-b）」

**2. 詢問基本資訊（一次問清楚）**
```
請提供以下資訊（有的填，沒有的留空）：
1. 甲方名稱：
2. 專案類型：新開發 / 系統擴充 / 維護
3. 預計時程：
4. 主要技術棧（若已知）：
5. 一句話描述這個專案要做什麼：
```

**3. 建立資料夾結構（含所有薄索引）**
在 `projects/{專案名稱}/` 下建立：

```
00-overview.md                    （填入收集的資訊）
01-requirements/
  functional-index.md             ← 薄索引 L1（模組目錄）
  functional/
    README.md                     ← 說明三層讀取結構（L1模組→L2模組Quick Context→L3 REQ掃描表）
  non-functional.md               （空白模板）
  _pending.md                     （含 Quick Context 優先級摘要頭）
  _inferred.md                    （含 Quick Context 風險摘要頭）
02-architecture/
  arch-index.md                   ← 薄索引（元件地圖）
  system-design/
    README.md                     ← 說明元件分檔結構
  api-contracts/
    index.md                      ← 薄索引（端點群組目錄）
    README.md                     ← 說明端點群組結構
03-client-context/
  stakeholders.md                 （含 Quick Context 決策者摘要頭）
  existing-system.md              （含 Quick Context 關鍵限制頭）
  domain-knowledge.md             （含 Quick Context 關鍵字頭）
04-decisions/
  ADR-index.md                    ← 薄索引（空白模板）
  ADR-000-template.md             （建立新 ADR 時複製）
05-dev-notes/
  _index.md                       ← 薄索引（空白模板）
06-qa-testing/
  bugs-active.md                  ← 薄索引（空白模板）
CHANGELOG.md                      （初始版本）
```

各薄索引在建立時為空白模板；後續由 `/ingest`、`/bug`、`/save` 指令自動維護內容。若是「擴充案」（既有系統），特別提醒：
- `existing-system.md` 必填，越詳細越好
- 建議立即執行 `/reverse-engineer` 填充 `_inferred.md`

**4. 更新 wiki/index.md**
將新專案加入「進行中的專案」表格。

**5. 更新 wiki/hot.md**
記錄新專案已建立，設為當前活躍專案。

**6. 完成回報**
```
✅ 專案 [{名稱}] 建立完成

📂 結構：projects/{名稱}/
⚡ 薄索引已建立：functional-index / arch-index / ADR-index / dev-notes/_index / bugs-active
📋 下一步：
  1. 將甲方文件放入 _inbox/，執行 /ingest 自動解析並填充 functional-index
  2. 確認非功能需求：01-requirements/non-functional.md
  3. 若為擴充案：填寫 existing-system.md，執行 /reverse-engineer
```
