# Phase 4：跨專案知識庫健康

掃描 `knowledge/` 目錄的整體健康狀況：

## patterns/index.md
```
- 總條目數：{N}
- status=validated：{N} 條
- status=experimental：{N} 條
- status=deprecated：{N} 條
- 缺少 tags 的條目：{N} 條
- validated 但 projects 為空：{N} 條（格式違規）
```

## lessons-learned/index.md
```
- 總條目數：{N}
- 有「納入系統守衛」記錄的：{N}/{Total}
- 缺少「預防方式」的：{N} 條
```

## tech-stack/index.md
```
- 第三方服務條目數：{N}
- 記錄完整度 ⬜ 空白的服務：{N} 個（列出服務名稱）
```

## wiki/index.md 一致性
```
- 在 wiki/index.md 列為「進行中」但 projects/ 下不存在的專案：{N} 個
```

## 檔案歸屬一致性（誤放偵測）
```
knowledge/patterns/ 下非 index.md 的檔案，標頭應為 PAT- 開頭；
knowledge/lessons-learned/ 下非 index.md 的檔案，標頭應為 LESSON- 開頭。
不符 → 🟡 警告：「{檔案路徑} 的內容類型（{實際 ID}）與所在目錄不符，疑似誤放」
```

輸出格式：
```
━━━ 知識庫健康統計 ━━━
設計模式：{N} 條 / 完整 {N} / 不完整 {N}
教訓記錄：{N} 條 / 完整 {N} / 不完整 {N}
第三方服務：{N} 個 / 記錄完整 {N} / 空白 {N}
```

→ 完成後讀取 `_health-check/report.md`（若完整診斷模式）
