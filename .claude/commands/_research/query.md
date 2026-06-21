# Phase 2：構建精準搜索查詢

根據約束輪廓，將問題改寫為精準查詢。

## 查詢改寫格式

```
原始問題：「{使用者的問題}」

改寫後：
  主查詢：「{技術關鍵字} {框架版本} {環境} best practice {年份}」
  補充查詢：「{方案名} vs {方案名} {環境} compatibility」
  排除條件：「NOT Docker NOT Linux-only NOT requires {不支援的依賴}」
```

## 範例

```
原始問題：「如何實作用戶認證」

改寫後（假設：PHP 7.4 / Laravel / MySQL 5.7 / Windows Server）：
  主查詢：「JWT authentication PHP Laravel MySQL 5.7 Windows Server best practice 2024」
  補充查詢：「Laravel Sanctum vs Passport Windows IIS deployment compatibility」
  排除條件：「NOT Docker NOT Linux-only NOT requires Redis」
```

約束輪廓中的限制越具體，查詢改寫越精準。

→ 完成後讀取 `_research/search.md`
