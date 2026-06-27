# /save 協作狀態更新

> 在 `_save/gather.md` Step 3（ADR）之後執行。
> 前提：`projects/{專案名稱}/collab/` 資料夾存在。

---

## Step 1：確認目前鎖定狀態

讀取 `projects/{專案名稱}/collab/{initials}.md`（只讀自己的），顯示目前鎖定的項目。

若 `collab/` 資料夾不存在 → 跳過，繼續 `_save/index.md`。

## Step 2：詢問新鎖定

```
🔒 協作狀態更新

本次 session 涉及以下項目：
  REQ：{從 dev-notes 推斷的 REQ 列表}
  元件/API 群組：{從 dev-notes 推斷的 02-architecture/ 異動列表}

是否需要將以下項目加入你的鎖定？
（鎖定代表你還在處理，其他工程師 BEFORE CODING 時會收到警告）

  [1] REQ-FXXX（{描述}）
  [2] {元件或 API 群組名稱}（{描述}）
  [全部] 全部鎖定
  [跳過] 不更新
```

依使用者選擇，在 `active_work` 中新增或保留對應條目：
```markdown
| {類型} | {項目} | {位置} | {YYYY-MM-DD} | {本次工作簡述} |
```

## Step 3：詢問解鎖

若目前 `active_work` 中有你名下的項目：

```
✅ 以下項目是否已完成，可以解鎖？
（解鎖後其他工程師的 BEFORE CODING 不再收到衝突警告）

  [1] REQ-FXXX（鎖定於 {日期}）
  [2] {元件或 API 群組名稱}（鎖定於 {日期}）
  [全部] 全部解鎖
  [保留] 全部保留
```

依選擇從 `active_work` 中移除對應條目。

## Step 4：寫入 collab/{initials}.md（只寫自己的檔案）

完整替換 `projects/{專案名稱}/collab/{initials}.md`：
- 新增鎖定條目（含類型、今日日期）
- 移除解鎖條目
- 更新 `updated` 欄位為今日日期
- **不觸碰其他工程師的檔案**（零衝突設計）

## Step 5：完成提示

```
✅ collab/{initials}.md 已更新

  🔒 新鎖定：{項目列表 或「無」}
  🔓 已解鎖：{項目列表 或「無」}
  目前你鎖定中：{完整鎖定項目列表}
```

→ 繼續 `_save/index.md`
