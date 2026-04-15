# 食品營養標示分析系統 - 部署資訊

## 部署平台
GitHub Pages

## GitHub Repo
https://github.com/jacky5453-beep/nutrition-system

## 線上網址
https://jacky5453-beep.github.io/nutrition-system/

## 部署指令
```bash
cd "/Users/jacky/Desktop/claude/claude code/食品營養標示分析系統"
git add -A && git commit -m "描述" && git push origin main
# GitHub Pages 自動部署（來源：main 分支 / 根目錄）
```

## 資料庫
- **Supabase**（主要）：`https://btnyditozvaqcxthomjk.supabase.co`
  - 分析歷史記錄、翻譯詞庫、展開庫 雲端同步
- **localStorage**（備援）：Supabase 連線失敗時自動降級

## 環境變數
無（API Key 由使用者在前端輸入，存於 localStorage）

## 最後部署日期
2026-04-15
