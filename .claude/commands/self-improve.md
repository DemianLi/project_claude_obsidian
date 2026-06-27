---
description: 從 session 模式學習，更新 patterns 與 lessons-learned
---
# /self-improve — 知識庫自我優化迴圈

## 觸發方式
```
/self-improve              （全面掃描）
/self-improve [專案名稱]   （只掃描特定專案）
```

## 說明
這是閉環的核心：定期執行，讓知識庫從實戰中持續優化。
建議每完成一個功能模組、或每隔 1-2 週執行一次。

## 前置條件
```
[ ] projects/{專案}/05-dev-notes/ 存在且有內容（供掃描）
```

## 執行序列（每次只讀當前 Phase 的子文件）

| Phase | 讀取 | 說明 |
|-------|------|------|
| 1 | `_self-improve/scan.md` | 掃描最近 30 天的 dev-notes，提取重複問題與解法 |
| 2 | `_self-improve/patterns-tech.md` | 提取可複用模式 + 第三方服務踩坑 |
| 3 | `_self-improve/lessons.md` | 提取通用教訓 + 更新甲方偏好 |
| 4 | `_self-improve/health-report.md` | 健康檢查 + 生成改善報告 + 更新 wiki |

## 互動原則
- 每個建議寫入動作都**必須詢問使用者確認**
- 自動執行：Phase 4 的 wiki/hot.md 和 wiki/log.md 更新
