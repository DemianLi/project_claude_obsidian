# Phase 3：寫入（只寫使用者確認的內容）

---

## 3-0：背景知識 → `03-client-context/`

依類別 append 至對應檔案（`stakeholders.md` / `existing-system.md` / `domain-knowledge.md`）。

若同一關係人已有記錄 → **合併更新**，不新增重複條目。
若與既有背景知識有出入 → **標記衝突**，等使用者確認，不自動覆寫。

**對帳：清理已解決的 _pending / _inferred**

```markdown
<!-- 完全解決 → _pending.md 加狀態 -->
### ~~PENDING-XXX：{標題}~~
**狀態**：✅ 已解決  **解決方式**：由 REQ-FXXX 涵蓋  **日期**：{YYYY-MM-DD}

<!-- 推測升格 → _inferred.md 加狀態 -->
### ~~INF-XXX：{標題}~~
**狀態**：✅ 已驗證  **升格為**：REQ-FXXX  **日期**：{YYYY-MM-DD}
```

部分解決：原條目拆分為已解決部分（標記 ✅）+ 新 PENDING-XXX 繼承剩餘問題。

## 3-1：明確需求 → `functional.md`

```markdown
## REQ-F{XXX}：{需求名稱}

**狀態**：✅ 已確認甲方
**確認日期**：{YYYY-MM-DD}
**來源文件**：{文件名稱} 第 {X} 頁
**提出人**：{甲方姓名/角色}（若已知）
**合約版本**：原始合約 v1.0
**清晰度**：🟢 明確

### 描述
{需求描述}

### 驗收條件
- [ ] {條件一}
- [ ] {條件二}
```

> ⚠️ 寫入前確認 `scope.md`：不在原始合約範圍 → 先執行 `/cr`。

## 3-2：模糊需求 → `_pending.md`

```markdown
## PENDING-{XXX}：{標題}
**原文**：{原始文字}  **來源**：{文件} 第 X 頁
**問題**：{缺少什麼}
**建議問甲方**：
> {可直接複製給甲方的問題}
**狀態**：等待回覆
```

若 `_pending.md` 已存在 → **append**，不覆寫舊的。

## 3-3：衝突更新

使用者選擇以新內容更新既有需求時，在原 REQ 加入：
```markdown
> **⚠️ 版本更新**：{YYYY-MM-DD} 依 {文件名} 更新，原版本：{舊描述}
```

## 3-4：矛盾偵測（wiki 層 + 工程層交叉）

若本次解析內容與以下任一來源有**語意矛盾**：
- `wiki/concepts/` 或 `wiki/entities/` 中的既有結論
- `wiki/sources/` 中另一來源的描述

→ 在**兩個頁面**均加入 `[!contradiction]` callout（不靜默覆寫）：

```markdown
> [!contradiction] 與 [[{另一頁面}]] 衝突
> 本文說：{新來源的描述}
> [[{另一頁面}]] 說：{既有記錄的描述}
> 建議：確認哪個更新/更可靠後，手動更新並移除此 callout。
```

**矛盾判斷標準（只標記明確衝突，不標記「補充」）：**
- 同一技術的版本號不同 → ✅ 矛盾
- 同一 API 的行為描述相反 → ✅ 矛盾
- 一個說「支援」一個說「不支援」→ ✅ 矛盾
- 一個說「建議用 A」一個說「建議用 B」（同場景）→ ✅ 矛盾
- 補充說明、不同面向的描述 → ❌ 不是矛盾

## 3-5：更新 .raw/.manifest.json

若本次來源來自 `.raw/`（URL 輸入或實體文件），
在 `.manifest.json` 補填：
```json
"ingested_at": "{YYYY-MM-DD}",
"pages_created": ["wiki/sources/{頁面}.md", ...],
"pages_updated": ["wiki/index.md", ...]
```

→ 完成後前往 `_ingest/report.md`（Phase 4）
