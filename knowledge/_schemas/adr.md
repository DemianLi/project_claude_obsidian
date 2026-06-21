---
type: schema
entity: ADR
version: 1.0
updated: 2026-06-21
---

# Schema：ADR（架構決策記錄）

> `/save` 步驟 3、`/architecture` 指令以此為格式參考。
> BEFORE CODING 步驟 6 讀取 `04-decisions/` 時，以此 schema 驗證格式。

---

## 完整格式

```markdown
---
type: adr
id: ADR-{NNN}
status: proposed | accepted | deprecated | superseded
date: YYYY-MM-DD
superseded_by: ADR-{NNN}  # 只有 superseded 時填
tags: [{tag1}, {tag2}]
affects_reqs: [REQ-F{XXX}, REQ-F{YYY}]  # 此決策影響哪些需求
---

# ADR-{NNN}：{決策標題（動詞 + 名詞，例：選用 JWT 而非 Session）}

## 背景

{什麼力量、約束、或需求促使了這個決策？技術環境限制、甲方要求、效能需求等。1-3 段。}

## 考慮過的選項

### 選項 A：{名稱}

**優點：**
- {優點一}

**缺點：**
- {缺點一}

### 選項 B：{名稱}

**優點：**
- {優點一}

**缺點：**
- {缺點一}

## 決策

**選擇：{選項 X}**

{選擇這個選項的理由，2-3 句話。這裡要說「為什麼這個選項比其他選項更適合這個情境」}

## 後果

**因此變得更容易的事：**
- {後果一}

**因此需要接受的代價：**
- {後果一}

**未來需要重新評估的時機：**
- {例：若甲方升級到支援 X 時，重新評估是否改用 Y}
```

---

## 必填欄位

| 欄位 | 必填 | 說明 |
|------|------|------|
| frontmatter `id` | ✅ | ADR-{NNN}，三位數字，同專案內唯一 |
| frontmatter `status` | ✅ | 見有效狀態值 |
| frontmatter `date` | ✅ | YYYY-MM-DD |
| `## 背景` | ✅ | 解釋為什麼需要這個決策 |
| `## 決策` | ✅ | 明確宣告選擇了什麼 |
| `## 後果` | ✅ | 必須有「後果」section，且包含「代價」子項 |
| `## 考慮過的選項` | ⬜ 選填 | 有替代方案時填；若只有一種做法，可省略 |

---

## 有效 status 值

| status | 含義 | Claude 的行為 |
|--------|------|--------------|
| `proposed` | 尚在討論，未定案 | 不視為決策，不強制遵循 |
| `accepted` | 已定案，正在執行 | **不得推翻**，如需修改必須開新 ADR |
| `deprecated` | 不再適用，但沒有直接替代 | 提醒此決策已過期，建議重新評估 |
| `superseded` | 已被 `superseded_by` 中的 ADR 取代 | 遵循新 ADR，舊 ADR 只作歷史參考 |

---

## 健康檢查規則（供 /health-check 使用）

一個 ADR 被視為「不健康」如果：
- 缺少 frontmatter 或 frontmatter 缺少 `id`、`status`、`date`
- `status` 不在有效值列表
- 缺少 `## 背景`（沒有背景的決策不可信）
- 缺少 `## 決策`（沒有明確決策的 ADR 沒有意義）
- 缺少 `## 後果`（沒有後果分析的決策可能被輕易推翻）
- `status: superseded` 但沒有 `superseded_by` 欄位
