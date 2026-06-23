# Phase 0：輸入格式偵測

判斷輸入形式，路由至對應前處理，再進入 Phase 1。

```
輸入類型判斷（可多選，均可與其他條件同時發生）：

① 圖片（截圖 / 手寫標注 / Mockup / 流程圖）
   → 前往 _ingest/input-visual.md（0-A）

② 結構化表格（CSV / Excel / 貼上表格）
   → 前往 _ingest/input-structured.md（0-B）

③ 非中文文件（英文 / 日文 / 其他）
   → 前往 _ingest/input-multilang.md（0-C）
   （可與 ①②④⑥ 同時觸發）

④ 大型文件（≥ 30 頁 / ≥ 80,000 字元）
   → 前往 _ingest/input-large.md（0-D）
   （優先處理：0-D 控制分批節奏，0-C 在每批內翻譯）

⑤ 純文字 / Markdown，小型（< 30 頁）
   → 直接進入 Phase 1：_ingest/parse.md

⑥ URL（https:// 開頭）
   → 前往 _ingest/input-url.md（0-F）
   抓取網頁 → 存入 .raw/articles/ → 進標準流程
   （可與 ③ 同時觸發：若英文頁面 → 同步進 0-C）
```

> **組合範例**：
> - 200 頁英文 SRS → ④ + ③ → input-large.md + 每批翻譯依 input-multilang.md
> - `https://redis.io/docs/` → ⑥ + ③ → input-url.md 抓取 → input-multilang.md 翻譯

前置確認後，所有路徑最終都進入：`_ingest/parse.md`（Phase 1）

**Delta 檢查（所有路徑適用）：**
若 `.raw/.manifest.json` 存在，且輸入來源（hash）已記錄且未變更
→ 告知「此來源已解析過（{日期}），若要強制重新解析請加 `--force`」並停止。
