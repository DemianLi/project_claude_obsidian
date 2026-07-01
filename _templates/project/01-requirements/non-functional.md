---
type: non-functional-requirements
project: {project_name}
updated: {YYYY-MM-DD}
---

# 非功能需求

---

## 效能 (Performance)

| 指標 | 要求 | 測量方式 |
|------|------|----------|
| 回應時間 | API < {X}ms (P95) | — |
| 並發用戶 | 支援 {N} 個同時在線 | — |
| 資料量 | 初始 {N} 筆，年增長 {X}% | — |

---

## 安全 (Security)

- [ ] 身份驗證機制：{JWT / Session / OAuth}
- [ ] 授權模型：{RBAC / ABAC / 其他}
- [ ] 資料加密：{傳輸 TLS / 靜態加密}
- [ ] 敏感資料：{描述哪些資料需要特別保護}
- [ ] 合規要求：{個資法 / GDPR / 其他}

---

## 可用性 (Availability)

- SLA 要求：{99.9%} uptime
- 計畫性維護：{每周/每月} {時間窗口}
- RTO（復原時間目標）：{X 小時}
- RPO（復原點目標）：{X 小時}

---

## 相容性 (Compatibility)

- 瀏覽器支援：{Chrome 最近 2 版 / 其他}
- 行動裝置：{是 / 否 / RWD}
- 現有系統整合：詳見 [[../03-client-context/existing-system]]

---

## 部署與維運

- 部署環境：{雲端 / 地端 / 混合}
- 監控要求：{日誌保留期 / 告警通知}
- 備份策略：{頻率 / 保留期}

---

## 其他限制

- {甲方特有限制，例如：不可使用某些第三方服務、必須使用特定版本等}
